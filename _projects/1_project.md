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

## Cellular Automata Foundation

This project is fundamentally built on cellular automata principles, where:

- The simulation space is divided into a discrete grid of cells
- Each cell exists in one of several possible states (empty, particle, or structure)
- Evolution occurs in discrete time steps according to well-defined rules
- The state of each cell depends only on its previous state and the states of neighboring cells

The cellular automaton framework provides several advantages for modeling diffusion-limited aggregation:

- **Emergent Complexity**: Simple local rules lead to complex global patterns
- **Discrete Nature**: Perfect for digital implementation and analysis
- **Parallelizability**: Each cell update can be computed independently
- **Rule-Based Evolution**: The system evolves deterministically from initial conditions

The Margolus neighborhood used in this implementation is a specialized cellular automaton technique that divides the grid into 2×2 blocks and applies transformations to these blocks, alternating the block boundaries between time steps. This approach preserves important physical properties like conservation laws while enabling the complex dynamics needed for realistic dendrite formation.

Unlike the more common von Neumann neighborhood (which considers only the four adjacent cells: north, east, south, and west), the Margolus neighborhood operates on 2×2 blocks rather than individual cells. This distinction is crucial for our simulation because:

1. The von Neumann neighborhood typically leads to grid artifacts with strong directional bias along the cardinal directions
2. The Margolus approach allows for conservation of particles during diffusion, which is physically accurate
3. While von Neumann neighborhoods process each cell individually based on fixed adjacent cells, Margolus neighborhoods process blocks of cells together, allowing for more complex interactions
4. The alternating block boundaries in Margolus shuffling prevent the grid orientation from influencing the diffusion pattern, resulting in more realistic isotropic diffusion

This difference is particularly important for diffusion-limited aggregation, where the von Neumann approach would create unrealistic "diamond-shaped" growth patterns aligned with the grid, while the Margolus approach produces the natural-looking fractal structures we observe in real dendrite formation.

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

## Relevance

This dendrite simulation approach has relevance across several scientific and engineering domains where diffusion-limited processes are fundamental:

### Neuromorphic Computing
Our diffusion-limited aggregation model is particularly relevant to neuromorphic computing because the physical growth of artificial neural networks can be governed by similar principles. In both our simulation and physical neuromorphic systems, the random walk of particles mimics how material precursors diffuse through a medium before deposition. The directional bias we've implemented parallels how electric fields guide the growth of conductive pathways in physical neural networks. This is crucial for creating self-organizing hardware that can form functional connections without explicit programming. The Margolus neighborhood approach we use captures the local interaction rules that determine how these structures branch and connect, similar to how memristive devices form conductive filaments through ion migration—a diffusion-driven process that changes resistance states based on applied voltage and material properties.

### Biological Neural Development
Neural development is fundamentally a diffusion-limited process where our simulation approach excels. Dendrite growth in biological neurons follows a process remarkably similar to our model: growth factors diffuse through the extracellular matrix, creating concentration gradients that guide dendrite extension. Our simulation's stochastic diffusion with directional bias accurately captures how these chemical gradients influence growth cone navigation. The fractal patterns emerging in our model mirror the self-similar branching observed in real neurons, where each branching decision is influenced by local molecular interactions. The computational efficiency of our Margolus shuffling technique allows us to simulate these complex diffusion dynamics at scales relevant to actual neural development, making it possible to model how subtle changes in the diffusion environment can lead to dramatically different neural architectures—a key insight for understanding both normal development and pathological conditions.

### Semiconductor Manufacturing
Semiconductor fabrication increasingly relies on bottom-up self-assembly processes that are inherently diffusion-limited, making our simulation approach highly relevant. In processes like chemical vapor deposition, precursor molecules diffuse through a gas phase before depositing on a substrate—exactly the type of random walk with sticking rules that our model simulates. The horizontal bias field in our implementation mirrors how electric fields or temperature gradients can direct the growth of nanowires and other semiconductor structures. Our approach is particularly valuable because it captures the stochastic nature of these processes while still accounting for directional influences, allowing manufacturers to predict how process parameters will affect the resulting structures. The emergent fractal dimensions in our simulation correspond directly to the surface roughness and porosity of deposited films, which critically affect semiconductor device performance through properties like electron mobility and optical characteristics.

### Electropolymerization
Electropolymerization represents perhaps the most direct application of our diffusion-limited aggregation model. During this process, monomers diffuse through an electrolyte solution toward an electrode where they undergo oxidation and subsequent polymerization—a process perfectly captured by our particle diffusion and aggregation rules. The horizontal bias in our model directly corresponds to the electric field gradient that drives this process, with stronger fields creating more directionally elongated polymer structures. Our simulation accurately reproduces the dendritic growth patterns observed in real electropolymerization, where polymer chains branch out from the electrode surface in fractal patterns. The diffusion-limited nature of this process creates concentration gradients that our model captures through the probabilistic movement of particles. By adjusting parameters like diffusion rate and field strength, our simulation can predict how changes in electrolyte concentration, applied voltage, and electrode geometry will affect the resulting polymer morphology—insights that are difficult to obtain through experimental methods alone but crucial for optimizing electropolymerization for applications in sensors, actuators, and energy storage devices.

### Self-Organizing Systems in Ecology
Our dendrite simulation approach provides remarkable insights into self-organizing ecological systems, particularly in vegetation pattern formation in semi-arid ecosystems. These ecosystems exhibit striking regular patterns of vegetation alternating with bare soil—a phenomenon driven by diffusion-limited resource distribution. Our model excels at capturing this process because the core mechanism is fundamentally similar: water and nutrients diffuse through soil, with plants acting as "sticky" aggregation points that deplete resources in their immediate vicinity while benefiting from resources at greater distances. The horizontal bias component of our simulation perfectly models how topographical gradients influence water flow and subsequent vegetation growth patterns. What makes our approach particularly powerful for modeling these systems is the Margolus neighborhood implementation, which efficiently captures the short-range facilitation (plants helping nearby plants by improving soil conditions) and long-range competition (plants competing for scarce water resources) that characterize these ecosystems. The emergent fractal patterns in our simulation closely match the spatial distributions observed in real tiger bush, spotted vegetation, and labyrinth patterns found in nature. By adjusting diffusion rates and bias strength, our model can predict how climate change might alter these self-organizing vegetation patterns—a critical tool for understanding ecosystem resilience and potential tipping points in these fragile environments.

### Cellular Automata Theory and Applications
This project contributes to the broader field of cellular automata research by demonstrating how specialized CA rules can model complex physical phenomena. While traditional cellular automata like Conway's Game of Life use fixed neighborhood patterns, our implementation showcases the power of the Margolus neighborhood for modeling physical systems with conservation laws. The project demonstrates how cellular automata can bridge the gap between discrete computational models and continuous physical processes, providing insights into how simple rules can generate complex emergent behaviors. Our implementation also shows how cellular automata can be modified to incorporate directional biases while maintaining their fundamental discrete nature, expanding the theoretical toolkit for CA researchers and practitioners.

## Future Work

Potential extensions to this project include:
- Implementing 3D diffusion-limited aggregation
- Adding multiple bias fields with different orientations
- Incorporating temperature effects on the diffusion process
- Parallelizing the simulation for larger scale structures
- Exploring different cellular automaton rule sets to model various physical constraints
- Developing hybrid models that combine cellular automata with differential equations for multi-scale modeling

If you're interested in contributing or have questions about the implementation, please feel free to open an issue or submit a pull request on the GitHub repository.
