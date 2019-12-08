---
layout: post
title:  "Boundary Conditions for Seismic Imaging: The Computer and Geophysical Points of View"
date:   2019-12-08 01:12:32 +0200
categories: HPC programming
---

### Introduction:
Reverse Time Migration (RTM) is a powerful seismic imaging approach, widely used for migrating areas of complex structures of steep-dips and subsalt regions, despite its high computational cost. As in our work we are solving the isotropic acoustic  2nd order wave equation using explicit time domain finite differences (FD), we can identify the most computational part as follows : The FD kernel by itself , the boundary condition, the way we handle snapshots and the communication between domains.

Following previous work where we did show FD kernel optimizations and different techniques to keep the snapshots (with or without IO or compression), we are now reporting some results on boundary conditions taking into consideration the trade-offs between the geophysical effects and utilization of computational elements.Moreover, finding the optimal solution between computational cost and efficiency of a boundary condition algorithm and its effectiveness in attenuating unwanted energy.
 
Theoretically, waves propagate their extends to infinity or continue until vanishing. Unfortunately, this is not applicable in modeling a particular region since we truncate model to a computational grid modeling a region of interest. Absorbing all incoming energy at the boundaries of the computational grid mimic a real-life infinite media. Many approaches attempt to mimic different kinds of absorbing boundary conditions (ABC) e.g. Sponge, PML, random boundaries, etc.  

Here, we review 2 RTM implementations, in addition to the compression capable version. One is using the standard approach (2 propagations with in-memory snapshots of the full wavefield) covering Sponge and CPML boundary conditions, while the second implementation uses random velocity boundaries  that almost avoid IO but involves an extra propagation.
We already demonstrated,in our previous report, the efficiency tradeoff of those implementations so now we can typically balance the number of grid points in the damping area to find the best combination with respect to the efficiency of the rest of the RTM implementations and present a complete comparison of the damped energy with varying boundaries lengths.

### Boundary conditions:
