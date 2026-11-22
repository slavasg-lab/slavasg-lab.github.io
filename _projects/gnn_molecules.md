---
layout: page
title: GNNs for Molecules
description: Project thesis. One graph neural network for thermodynamic properties of pure compounds and mixtures
img: assets/img/projects/gnn_thumb.jpg
importance: 5
category: work
---

Project thesis at the Chair of Process Systems Engineering, RWTH Aachen (Prof. Alexander Mitsos, supervised by Jan Rittig), September 2024.
Team project with Bogdan Cherleniuk, Platon Kastrytski and Levon Keshishian.

Graph neural networks for structure–property prediction usually predict one or a few properties. We built a single model that predicts
internal energy, molar volume, enthalpy and isobaric heat capacity as functions of temperature and pressure, for pure compounds and for mixtures
with different numbers of components. The training data was generated with REFPROP.

{% include figure.liquid loading="eager" path="assets/img/projects/gnn_architecture.png" class="img-fluid rounded" %}

<div class="caption">
  The model has three stages: a GNN embeds each molecule, a second GNN combines the molecule embeddings into a mixture embedding, and an MLP
  predicts the properties from the mixture embedding together with temperature and pressure.
</div>

{% include figure.liquid loading="eager" path="assets/img/projects/gnn_mixture_fingerprint.png" class="img-fluid rounded" %}

<div class="caption">
  Mixture fingerprint for a three-component mixture: the molecular fingerprints become vertex features of a mixture graph, a graph
  convolution processes them, and the result is pooled into one vector.
</div>

The model generalises to new temperatures and pressures, but it is not accurate for molecules it has not seen or for mixtures with new
compositions. Neither multi-task learning nor building thermodynamic relations between the properties into the model gave a clear benefit in
this configuration.

{% include figure.liquid loading="eager" path="assets/img/projects/gnn_parity.png" class="img-fluid rounded" %}

<div class="caption">
  Parity plots on the test set for (a) a random split, (b) unseen mixtures and (c) unseen molecules.
</div>
