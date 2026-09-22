# sync3d | Quantum Geometric Alignment Engine

```text
============================================================
 [ S Y N C 3 D ] : QUANTUM GEOMETRIC ALIGNMENT ENGINE (V.0.1.0)
------------------------------------------------------------
 >> CORE BASE SYSTEM: HARDWARE-ACCELERATED MULTI-TRACE 3D
 >> EXTENSION EXPANSION: KATHARINA MARIA BRECHT (2026)
============================================================
```


> **Synchronized 3D Vector and Marker Animations in 'Plotly' via 'WebGL'**


`sync3d` is a lightweight, high-performance R package designed to bypass structural rendering limitations within multi-trace 3D animations in `plotly`.

By decoupling the data computing pipeline, it allows researchers and developers to simultaneously animate complex 3D topological frameworks (lines/edges) and dynamic physical states (markers/nodes) without 'UI' degradation or controller loss.

Note: This repository provides a minimal working example for engine testing. High-volume coordinate matrices required for large-scale visualizations are deliberately omitted to minimize package size.

## Installation

You can install the development version of `sync3d` from GitHub (once repository is live) with:

```r
# install.packages("devtools")
devtools::install_github("KatharinaBrecht-Quantum/sync3d")
```

## The Problem: Multi-Trace 3D Animation Limits in R
When attempting to animate two separate 3D traces (e.g., a static geometric wireframe model and a time-dependent quantum wave field changing colors) using the native R `plotly` structure, the engine loses synchronization across frames. This causes the animation to freeze, line paths to break, or 'UI' control elements (Play/Pause buttons) to completely malfunction.

## The Solution: Dual-Layer Pipeline Decoupling
`sync3d` resolves this constraint through a hardware-accelerated dual-layer execution pattern:
1. **R Environment:** Exclusively manages the high-efficiency matrix computation of animated particles/nodes (color, size, coordinates) and initializes the core 'plotly' frames.
2. **'WebGL' Injected Pipeline:** Injects a custom JavaScript layer via `htmlwidgets::onRender` directly into the browser. This handles the rendering of topological framework connections (lines/edges) directly on the GPU, synchronizing lines seamlessly with every animated state transition.

## Target Applications & Fields of Use

`sync3d` is designed as a domain-agnostic visualization utility. By enabling high-performance, synchronous multi-trace 3D animations, it serves critical visual computing needs in fields such as:

* **Crystallography & Materials Science:** Visualizing time-dependent structural phase transitions, lattice defects, and atomic displacement vectors within complex crystal frameworks.
* **Structural Biology & Biochemistry:** Simulating dynamic protein folding pathways, molecular docking interferences, and changing electrostatic potentials on macromolecular surfaces.
* **Quantum Chemistry & Particle Physics:** Mapping animated spatial probability densities, evolving wave functions, and topological resonance states.
* **Network Analysis & Graph Theory:** Rendering large-scale, interactive 3D network layouts where cluster states change dynamically over time.

## Quick Start Example

```r
library(plotly)
library(sync3d)

# 1. Define nodes/particles in 3D Space
nodes_df <- data.frame(
  x = c(0, 1, 0, -1, 0, 0),
  y = c(0, 0, 1, 0, 0, 0),
  z = c(1, 0, 0, 0, -1, 0)
)

# 2. Define edge connections (Indices of points to connect)
edge_matrix <- matrix(c(1,2, 1,3, 1,4, 1,6), ncol = 2, byrow = TRUE)

# 3. Create your animated plotly base (Markers only)
base_plot <- plot_ly(data = nodes_df, x = ~x, y = ~y, z = ~z, type = 'scatter3d', mode = 'markers')

# 4. Apply sync3d extension to render hardware-accelerated synchronized lines
final_plot <- add_synchronized_3d_edges(base_plot, edge_matrix)
final_plot
```

## Intention & Scientific Context

`sync3d` was originally conceptualized during the development of **`octawave`** (Spatial Octahedral Quantum Wave Functions). 

While `octawave` focuses on the mathematical simulation, spatial resonance fields, and structural 'MRI' slice generation of fullerene models, it encountered the native multi-trace 3D animation limits of R. `sync3d` was decoupled as an independent, generic extension to solve this specific technical bottleneck for the entire R community. 

For advanced quantum wave field visualizations and octahedral topologies, see the companion package:
* **octawave:** Spatial Octahedral Quantum Wave Functions (CRAN)

## Current Status & Active Development (WIP)

Notice: This repository is actively maintained and developed by the author as part of an ongoing academic research project into spatial quantum structures. 

* **Development Status:** Experimental / Active Core Engine.
* **Upcoming Extensions:** Integration of dynamic tetrahedral coordinate transformations and complex phase-amplitude mapping.
* **Academic Priority:** The underlying mathematical models and specific quantum wave field simulations are subject to an upcoming primary publication. If you wish to collaborate or benchmark against this engine, please contact the maintainer directly.

## License
This package is licensed under the GPL-3 License.
