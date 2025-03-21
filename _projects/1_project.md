---
layout: distill
title: Dendrite Networks
description: A cellular automaton model simulating dendritic growth with parallized diffusion. 
img: assets/img/projects/dendrites/dla_figure.png
importance: 1
category: work
related_publications: true
date: 2025-01-22
github_repo: https://github.com/lukasbongartz/dendrite_sim

authors:
  - name: Lukas Bongartz
---

I use a cellular automaton (CA) model to simulate the growth of dendretic structures in terms of diffusion-limited aggregation (DLA). The simulation uses Margolus shuffling, which allows for paralllization under conservation of information and isotropic diffusion. 

[GitHub repository](https://github.com/lukasbongartz/dendrite_sim).

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/dendrites/dla_gaussian_ac_field.GIF" title="Dendrite growth simulation" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Diffusion-limited aggregation under a horizintal AC bias (Gaussian around center). The colorbar shows normalized degree centrality. 
</div>

## Cellular Automata

In cellular automata models, we consider a discrete grid of cells, eaching having a finite set of possible states. The system evolves according to fixed rules based on local cell neighborhoods. There are multiple ways of how the neighborhood can be considered, for example in terms of the Von Neumann or Moore neighboorhod. 

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/dendrites/neighborhoods.png" title="Neighborhoods in Cellular Automaton" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Von Neumann, Moore, and Margolus neighborhood.
</div>

The Von Neumann neighborhood consists of a central cell and its four adjacent neighbors (up, down, left, right). The Moore neighboorhod extends to the eight surrounding cells, so including the diagonals. This is also what's used in [Conway's Game of Life](https://playgameoflife.com/). The Margolus neighborhood partitions the grid into 2×2 blocks and updates them synchronously. This partition shifts on alternating steps, allowing for reversible dynamics. 

## Margolus Shuffling

The Margolus shuffling algorithm follows these update rules:

{% highlight text %}
1. Divide the grid into 2×2 blocks:
   if time_step % 2 == 0:
       Start blocks at even coordinates (0,0), (2,0), etc.
   else:
       Start blocks at odd coordinates (1,1), (3,1), etc.
2. For each block:
   - Redistribute particles within the block according to update rules
   - Conserve the total number of particles
3. Advance to the next time step
4. Repeat
{% endhighlight %}

The key point is that the block updates are independent from one another, which allows us to parallelize. Meanwhile, it preserves local conservation and reversibility.

To model aggregation, we initilize the grid with a (fixed) seed in the center and randomly distributied (free) particles in a given density. The update rules are quite simple:

{% highlight text %}
For each free particle:
   - If any neighbor is part of aggregate:
       Join particle to aggregate
   - Else:
       Remain free for Margolus shuffling
{% endhighlight %}
We here consider only neighbors in the _Von Neumann neighborhood_ for sticking. Moving to larger numbers of particls, we get fractals of high complexity.


<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/dendrites/margolus.gif" title="Margolus shuffling" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/dendrites/dla_v0.gif" title="DLA with 100 particles" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Margolus shuffling and aggregation using Von Neumann neighborhood. Right: Diffusion-limited aggregation for a system of 100 free particles.
</div>


## Model Extension

We can now extend this model by introducing two additional parameter:
1. We introduce a bias, making diffusion more favorable along a certain axis.
2. We introduce a sticking probability, bringing the aggregation process closer to the one seen in natural systems.

#### 1. Diffusion under Bias

Within each $2 \times 2$ block, we consider a *horizontal* and a *vertical* pair, corresponding to the left/right and top/bottom cells. Transitions in each pair are biased by a field $\mathbf{F} = (F_x, F_y)$ with strength $\alpha$. For $F_x > 0$, the probability of a move to the right is defined as

$$
  p_{\text{right}} \;=\; \frac{ e^{\,\alpha \, F_x} }{ e^{\,\alpha \, F_x} \;+\; 1 }.
$$

For a move to the left, it follows

$$
  p_{\text{left}} = 1- p_{\text{right}} \;=\; \frac{ e^{-\alpha \, F_x} }{ e^{-\alpha \, F_x} \;+\; 1 }
$$
    Vertical moves would follow the same pattern using $F_y$.  





<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/dendrites/margolus_bias.png" title="Diffusion under bias" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/dendrites/dla_bias.gif" title="DLA under bias" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Diffusion under a horizontal bias. Right: Diffusion-limited aggregation under a bias (periodic boundary conditions).
</div>





Instead of assinging each of 

In each iteration

#### 2. Probabilistic Aggregation

## Network Analysis


## Parallels in Nature

While being computationally rather simple, this CA model is reminiscent of many processes throughout nature.

#### Dielectric Breakdown

...

#### Neuromorphic Computing
Our diffusion-limited aggregation model is particularly relevant to neuromorphic computing because the physical growth of artificial neural networks can be governed by similar principles. In both our simulation and physical neuromorphic systems, the random walk of particles mimics how material precursors diffuse through a medium before deposition. The directional bias we've implemented parallels how electric fields guide the growth of conductive pathways in physical neural networks. This is crucial for creating self-organizing hardware that can form functional connections without explicit programming. The Margolus neighborhood approach we use captures the local interaction rules that determine how these structures branch and connect, similar to how memristive devices form conductive filaments through ion migration—a diffusion-driven process that changes resistance states based on applied voltage and material properties.

#### Biological Neural Development
Neural development is fundamentally a diffusion-limited process where our simulation approach excels. Dendrite growth in biological neurons follows a process remarkably similar to our model: growth factors diffuse through the extracellular matrix, creating concentration gradients that guide dendrite extension. Our simulation's stochastic diffusion with directional bias accurately captures how these chemical gradients influence growth cone navigation. The fractal patterns emerging in our model mirror the self-similar branching observed in real neurons, where each branching decision is influenced by local molecular interactions. The computational efficiency of our Margolus shuffling technique allows us to simulate these complex diffusion dynamics at scales relevant to actual neural development, making it possible to model how subtle changes in the diffusion environment can lead to dramatically different neural architectures—a key insight for understanding both normal development and pathological conditions.

#### Semiconductor Manufacturing
Semiconductor fabrication increasingly relies on bottom-up self-assembly processes that are inherently diffusion-limited, making our simulation approach highly relevant. In processes like chemical vapor deposition, precursor molecules diffuse through a gas phase before depositing on a substrate—exactly the type of random walk with sticking rules that our model simulates. The horizontal bias field in our implementation mirrors how electric fields or temperature gradients can direct the growth of nanowires and other semiconductor structures. Our approach is particularly valuable because it captures the stochastic nature of these processes while still accounting for directional influences, allowing manufacturers to predict how process parameters will affect the resulting structures. The emergent fractal dimensions in our simulation correspond directly to the surface roughness and porosity of deposited films, which critically affect semiconductor device performance through properties like electron mobility and optical characteristics.

#### Electropolymerization
Electropolymerization represents perhaps the most direct application of our diffusion-limited aggregation model. During this process, monomers diffuse through an electrolyte solution toward an electrode where they undergo oxidation and subsequent polymerization—a process perfectly captured by our particle diffusion and aggregation rules. The horizontal bias in our model directly corresponds to the electric field gradient that drives this process, with stronger fields creating more directionally elongated polymer structures. Our simulation accurately reproduces the dendritic growth patterns observed in real electropolymerization, where polymer chains branch out from the electrode surface in fractal patterns. The diffusion-limited nature of this process creates concentration gradients that our model captures through the probabilistic movement of particles. By adjusting parameters like diffusion rate and field strength, our simulation can predict how changes in electrolyte concentration, applied voltage, and electrode geometry will affect the resulting polymer morphology—insights that are difficult to obtain through experimental methods alone but crucial for optimizing electropolymerization for applications in sensors, actuators, and energy storage devices.

#### Self-Organizing Systems in Ecology
Our dendrite simulation approach provides remarkable insights into self-organizing ecological systems, particularly in vegetation pattern formation in semi-arid ecosystems. These ecosystems exhibit striking regular patterns of vegetation alternating with bare soil—a phenomenon driven by diffusion-limited resource distribution. Our model excels at capturing this process because the core mechanism is fundamentally similar: water and nutrients diffuse through soil, with plants acting as "sticky" aggregation points that deplete resources in their immediate vicinity while benefiting from resources at greater distances. The horizontal bias component of our simulation perfectly models how topographical gradients influence water flow and subsequent vegetation growth patterns. What makes our approach particularly powerful for modeling these systems is the Margolus neighborhood implementation, which efficiently captures the short-range facilitation (plants helping nearby plants by improving soil conditions) and long-range competition (plants competing for scarce water resources) that characterize these ecosystems. The emergent fractal patterns in our simulation closely match the spatial distributions observed in real tiger bush, spotted vegetation, and labyrinth patterns found in nature. By adjusting diffusion rates and bias strength, our model can predict how climate change might alter these self-organizing vegetation patterns—a critical tool for understanding ecosystem resilience and potential tipping points in these fragile environments.

#### Cellular Automata Theory and Applications
This project contributes to the broader field of cellular automata research by demonstrating how specialized CA rules can model complex physical phenomena. While traditional cellular automata like Conway's Game of Life use fixed neighborhood patterns, our implementation showcases the power of the Margolus neighborhood for modeling physical systems with conservation laws. The project demonstrates how cellular automata can bridge the gap between discrete computational models and continuous physical processes, providing insights into how simple rules can generate complex emergent behaviors. Our implementation also shows how cellular automata can be modified to incorporate directional biases while maintaining their fundamental discrete nature, expanding the theoretical toolkit for CA researchers and practitioners.

## Future Work

Potential extensions to this project include:
- Implementing 3D diffusion-limited aggregation
- Adding multiple bias fields with different orientations
- Incorporating temperature effects on the diffusion process
- Parallelizing the simulation for larger scale structures
- Exploring different cellular automaton rule sets to model various physical constraints
- Developing hybrid models that combine cellular automata with differential equations for multi-scale modeling
