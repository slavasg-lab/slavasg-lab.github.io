---
layout: page
title: Diffusion Policy on Franka
description: Running a FastUMI diffusion policy on a Franka Panda, plus an experiment with depth input
img: assets/img/projects/franka_diffusion_policy.jpg
importance: 1
category: work
---

<!-- DRAFT. TODOs are HTML comments and do not render. Media slots are marked "MEDIA:". -->

TU Dresden, Jan – Apr 2026, about 20 h/week.
Python, PyTorch, Diffusion Policy, polymetis / libfranka, Depth-Anything-V2, SLURM.

## Overview

FastUMI is a handheld gripper for recording manipulation demonstrations, combined with a Diffusion Policy trained on those demonstrations.
I ported it to a Franka Panda with a Franka Hand. The published pour-water checkpoint ran on our robot without retraining: it grasped a bottle,
moved it over a cup and tilted it. I then trained a variant with monocular depth as an additional input. Training converged, but the policy
was shaky on the robot, and I didn't get to the bottom of why.

<!-- MEDIA: wrist-camera clip (5286…mp4) next to the external pour shot (IMG_2715). -->

## Background

I chose the project because I was interested in tactile sensing and in deploying learned policies on real hardware. FastUMI builds on
[UMI](https://umi-gripper.github.io/) and has since been extended with tactile sensing.

<!-- TODO: cite the FastUMI paper and the tactile follow-up by name. -->

The policy is a Diffusion Policy. It models the distribution of actions instead of regressing a single action, so when the demonstrations
contain several valid ways to do something (say, passing an obstacle on the left or on the right), it picks one of them instead of averaging
them.

## Setup on the Franka

The policy expects the camera and gripper of the handheld device. Our robot is a Franka Panda with a Franka Hand, controlled through polymetis.
What I had to add or change:

- A controller for the Franka Hand, plus a C++ benchmark of its low-level latency. A `move` command blocks for about 600 ms.
- A fix for a gripper deadlock in polymetis: when an object stopped the fingers from reaching the commanded width, the hand ignored all
  further commands, including `stop()`. My [fork](https://github.com/slavasg-lab/fairo-polymetis) aborts the previous motion before
  executing a new command, which makes it usable for a policy that streams gripper commands continuously.
- A transform chain from the polymetis flange frame (`link8`) through the hand TCP to the soft-fingertip TCP the policy uses. An earlier
  version had the base-to-end-effector rotation off by 90°, so the arm moved sideways.
- Recolouring the fingers in the camera image from orange to violet, since the training data was recorded with violet fingers.
- Connection and latency tests for arm and gripper, and inference-frequency benchmarks.

<!-- MEDIA: camera feed with orange fingers (IMG_2667) next to the recoloured version (IMG_2666 / 2668). -->
<!-- MEDIA: 5–10 s of the 90° frame bug (IMG_2686 or 2689). -->

## Pretrained policy

With this setup, the published pour-water checkpoint (trained by the original authors, not by me) ran on the Franka: it approached the bottle,
grasped it, moved to the cup and tilted the bottle over it.

<!-- MEDIA: 3D end-effector trajectory synced with the wrist-camera view. -->

## Depth input

I added depth from Depth-Anything-V2, estimated from the RGB camera:

- regenerated the training dataset with a depth map per frame,
- added depth as a second visual input to the model,
- trained on the university HPC cluster (about 40 h on 4×H100); the loss converged,
- added depth inference to the rollout loop, with the depth model on a second GPU.

<!-- TODO: check whether the FastUMI paper proposes depth via Depth-Anything; if so, say so here. -->
<!-- MEDIA: training loss curve, small. -->

On the robot the depth policy was shaky. From the logged rollouts, counting how often the end effector reverses direction per axis:

| Policy | Control rate | Direction reversals / s |
| ------ | ------------ | ----------------------- |
| RGB    | 10 Hz        | 2.5                     |
| Depth  | 10 Hz        | 9–12                    |
| RGB    | 5 Hz         | 1.4–2.1                 |
| Depth  | 5 Hz         | 3.9–7.3                 |
| Depth  | 2 Hz         | 0.9–1.3                 |

At the same control rate the depth policy reversed direction 2–5× as often. At 2 Hz it was smooth but barely moved. The sample is small
(5 RGB rollouts, 16 depth rollouts, many of them short).

<!-- MEDIA: clip of a shaky depth rollout (IMG_2746 / 2747) and an RGB-vs-depth trajectory plot. -->

## Possible causes

- Depth-Anything-V2 processes each frame independently, so the depth map changes from frame to frame even in a static scene.
- During rollout the depth model ran at its default input size (518 px), while the training data was generated at 448 px.
- Latency: about 0.7 s for observations, 0.34 s for inference, and about 600 ms per gripper command.
- Camera mount, scene, lighting and gripper all differ from the demonstrations, and I had no time to record my own data for fine-tuning.

The RGB policy also failed in some runs. In one, it treated a round contour on the table as the cup.

<!-- TODO: describe the cup-confusion run + add the clip. -->

From April a teammate worked with me on the rollout pipeline (latency, crashes caused by GPU power spikes) and on a fine-tuning plan.

<!-- TODO: teammate's name / link, if they agree. -->

## Next steps

Temporal smoothing of the depth maps, matching the depth resolution between training and rollout, and recording our own demonstrations.
The tactile part was out of scope given the time.

<!-- TODO: link to the GitHub repo. Before linking, revoke/remove the committed wandb key in docs/training/wandb.txt. -->
