---
layout: page
title: tum.ai Makeathon
description: planetree, a web app for monitoring deforestation from satellite images. Honourable mention at the TUM.ai Makeathon 2024
img: assets/img/projects/makeathon_planetree.jpg
importance: 4
category: work
---

TUM.ai Makeathon 2024 (April), osapiens challenge. Built in 36 hours by a team of four: Viacheslav Sydora, Danylo Movchan, Bohdan Popov and
Petro Laishev. Honourable mention.

[Devpost](https://devpost.com/software/osapiens-case) · Code: [client](https://github.com/KONTORA-SOLUTIONS/osapiens-client),
[API](https://github.com/KONTORA-SOLUTIONS/osapiens-api), [ML notebooks](https://github.com/KONTORA-SOLUTIONS/osapiens-ml-notebooks)

<div class="ratio ratio-16x9 mb-4" style="position: relative; padding-top: 56.25%;">
  <iframe
    src="https://www.youtube-nocookie.com/embed/fAMkcFnh4yc"
    title="planetree pitch"
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
    allow="accelerometer; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
  ></iframe>
</div>

planetree is a web app for monitoring deforestation. Users browse an interactive world map, select a region and click "scan". The app then
processes satellite images of that area and overlays a mask from a segmentation model: forest in green, deforested land in red. Users can also
drop pins where they have seen deforestation, which builds up a shared map of hotspots.

- **Frontend:** React with styled-components, HERE Maps for the map.
- **Backend:** FastAPI with PostgreSQL (SQLAlchemy).
- **Model:** a PyTorch computer-vision model, served as a separate microservice so that image processing does not block the main API.
- **Deployment:** Docker.

<!-- TODO: say which part you built (e.g. backend / API), if you want that on the page. -->
