---
layout: page
title: ML with Bricks
description: Open-source web platform and course that teaches machine learning to teenagers with LEGO robots
img: assets/img/projects/ml_with_bricks.jpg
importance: 3
category: work
---

Internship at the Max Planck Institute for Intelligent Systems, with Guner Dilsad Er and Michael Muehlebach. Published at RiE 2026.

[Platform](https://learning-and-dynamics.github.io/ml-with-bricks/) · [Video playlist](https://youtube.com/playlist?list=PLx1grFu4zAcwfKKJZ1Ux4LwRqaePCOA2J) ·
[Paper (arXiv)](https://arxiv.org/abs/2601.19376) · [Poster](/assets/pdf/LEGO_poster_RiE2026.pdf) ·
[BLE boilerplate code](https://github.com/slavasg-lab/lego-spikeprime-ble-boilerplate)

{% include figure.liquid loading="eager" path="assets/img/projects/ml_with_bricks_platform.jpg" class="img-fluid rounded" %}

Machine Learning with Bricks is a web platform and a two-day course for students aged 12 to 17. It uses LEGO SPIKE Prime kits and needs no
programming. Students collect data with the robots, train models in the browser and see the results on the robot. The browser talks to the
LEGO hub directly over Bluetooth Low Energy.

Each of the three robots covers one algorithm:

- **Fruit Detector:** classifies apples and bananas by colour and length with k-nearest neighbours.
- **Pitcher:** launches a table-tennis ball and learns the relation between motor speed and distance with linear regression.
- **Crawler:** learns a crawling motion with Q-learning.

In a pilot workshop with 14 students, self-reported understanding improved significantly in 6 of 8 topics, and the platform got high usability
ratings. The platform and the video course are freely available.
