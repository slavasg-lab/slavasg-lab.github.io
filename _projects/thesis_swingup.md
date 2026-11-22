---
layout: page
title: ILC for eMNS
description: Bachelor thesis. Learning-based control for a clinical electromagnetic navigation system
img: assets/img/projects/thesis_swingup.jpg
github: https://github.com/slavasg-lab/emns_invpend_swingup
importance: 2
category: work
---

Bachelor thesis (RWTH Aachen), carried out at the Max Planck Institute for Intelligent Systems (Learning and Dynamical Systems group) and the
Multi-Scale Robotics Lab at ETH Zürich. The thesis received the highest grade. The paper is shared first authorship with Jasan Zughaibi.

[Paper (arXiv)](https://arxiv.org/abs/2606.13915) · [Video](https://www.youtube.com/watch?v=1T4FVMYlteo) ·
[Code (ROS package)](https://github.com/slavasg-lab/emns_invpend_swingup)

<div class="ratio ratio-16x9 mb-4" style="position: relative; padding-top: 56.25%;">
  <iframe
    src="https://www.youtube-nocookie.com/embed/1T4FVMYlteo"
    title="Swing-up video"
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
    allow="accelerometer; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
  ></iframe>
</div>

Electromagnetic navigation systems (eMNS) steer magnetic devices such as catheters inside the body without contact. They are usually controlled
quasi-statically, close to equilibrium. I worked on dynamic trajectory tracking far from equilibrium, using a magnetically actuated inverted
pendulum on the clinical Navion eMNS as the test case. The controller works with torques and forces, so the same approach applies to other
magnetic devices.

The method combines:

- trajectory optimisation that accounts for the internal dynamics of the eMNS,
- time-varying LQR feedback around the optimised trajectory,
- iterative learning control (ILC), which uses data from previous trials and the system model to correct the feedforward command.

After each trial, an iteration-domain Kalman filter updates the disturbance estimate, and the next feedforward input is computed by solving a
constrained convex optimisation problem. Once the pendulum is close to upright, a separate LQR controller balances it.

{% include figure.liquid loading="eager" path="assets/img/projects/thesis_control_loop.jpg" class="img-fluid rounded" %}

<div class="caption">
  Control architecture: trajectory tracking with ILC feedforward and time-varying LQR feedback, switching to a balancing controller near the
  upright position.
</div>

LQR alone did not achieve the swing-up because of effects in the magnetic actuation that the model does not capture. With ILC, the pendulum
swung up within six iterations. The correction learned by ILC closely matched the torque error predicted by a high-fidelity calibration of the
magnetic field model.
