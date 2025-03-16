---
layout: page
title: Dendrite Networks
description: Simulation of Dendrite Growth with Diffusion-Limited Aggregation
img: assets/img/dla_gaussian_ac_field.GIF
importance: 1
category: work
related_publications: true
---

# Dendrite Networks with Diffusion-Limited Aggregation

This project implements a cellular automaton model for simulating dendrite growth through diffusion-limited aggregation (DLA). The simulation creates beautiful, fractal-like structures that resemble natural dendrite formations.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/dla_gaussian_ac_field.GIF" title="Dendrite growth simulation" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Visualization of dendrite growth using diffusion-limited aggregation with a horizontal bias field.
</div>

## Key Features

- **Margolus Shuffling Algorithm**: Implements efficient, isotropic diffusion by using the Margolus neighborhood approach
- **Directional Bias**: Introduces a horizontal bias field to simulate preferential growth along a specific axis
- **Tunable Parameters**: Allows for experimentation with different growth conditions and field strengths
- **Visualization**: Real-time visualization of the growing dendrite structures

## Technical Implementation

The simulation uses a cellular automaton approach where particles move randomly through diffusion until they encounter and stick to an existing structure. The Margolus shuffling algorithm is particularly important as it ensures:

1. Isotropic diffusion (equal probability in all directions)
2. Conservation of particle number
3. Computational efficiency

<div class="row">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/margolus_diagram.jpg" title="Margolus neighborhood diagram" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/dla_closeup.jpg" title="Close-up of dendrite structure" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Illustration of the Margolus neighborhood used for particle diffusion. Right: Close-up view of the fractal-like structure that emerges.
</div>

## Horizontal Bias Implementation

One of the novel aspects of this implementation is the introduction of a horizontal bias field. This creates directionally-biased growth that mimics natural systems where external forces (like electric or magnetic fields) influence dendrite formation.

The bias is implemented by modifying the transition probabilities in the diffusion process, making particles more likely to move along the horizontal axis. This results in elongated structures that grow preferentially in the horizontal direction.

## Results and Applications

The resulting structures exhibit fascinating fractal properties with potential applications in:

- Modeling electrodeposition processes
- Understanding crystal growth patterns
- Simulating neural dendrite formation
- Generating biologically-inspired artificial structures

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/dla_comparison.jpg" title="Comparison of different bias strengths" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Comparison of dendrite structures with different horizontal bias field strengths.
</div>

## Code and Implementation

The simulation is implemented in Python, using NumPy for efficient array operations and Matplotlib for visualization. The core of the algorithm involves:

1. Initializing a grid with seed particles
2. Implementing the Margolus shuffling for particle diffusion
3. Applying sticking rules when particles encounter the growing structure
4. Adding the horizontal bias field to influence growth direction

You can explore the full implementation in the [GitHub repository](https://github.com/lukasbongartz/dendrite_sim).

## Future Work

Potential extensions to this project include:
- Implementing 3D diffusion-limited aggregation
- Adding multiple bias fields with different orientations
- Incorporating temperature effects on the diffusion process
- Parallelizing the simulation for larger scale structures

If you're interested in contributing or have questions about the implementation, please feel free to open an issue or submit a pull request on the GitHub repository.
