---
layout: page
title: Component-Level Optimization of an Intelligent Reflecting Surface
description: Circuit-level PSO optimization for IRS beamforming that outperforms the reference paper's phase-model baseline by 38.4%
img: assets/img/projects/irs-pso.png
importance: 1
category: research
github: https://github.com/doremonn2847/IRS-project-analysis
---

Final project for the _Electronics for IT_ course (MiniProject20252), reproducing and extending Abeywickrama et al., "Intelligent Reflecting Surface: Practical Phase Shift Model and Beamforming Optimization" (IEEE Trans. Commun. 68(9), 2020).

Instead of optimizing the paper's abstract per-element phase shift θₙ — with reflection amplitude tied to it through an empirical curve fitted to one measured element — this project removes that intermediate model entirely and optimizes the physical circuit directly. For each of the _N_ IRS elements, the shunt inductance, series inductance, varactor capacitance, and loss resistance become decision variables, with the reflection coefficient computed straight from element impedance. This turns the problem into a 4*N*-dimensional non-convex optimization, solved with a memetic particle swarm optimizer (constriction PSO with an APSO-style elitist perturbation, seeded by a phase-aligned coordinate-ascent pass, refined with L-BFGS-B).

**Result:** across 500 Monte Carlo channel realizations, the proposed component-level PSO reaches 97.3% of the ideal (lossless) IRS's rate — beating the paper's phase-model alternating optimization baseline (70.3%) by 38.4 percentage points. The gain holds from _N_ = 10 to _N_ = 80 elements (a 320-dimensional search space at the top end) and across the full AP–user distance sweep tested.

The full report documents the system model, optimizer design, five experiments, and — deliberately — the design mistakes made along the way, including a fixed-budget bug that made the 4-variable search underperform the 2-variable one despite a strictly larger feasible set.

[Code, report, and full results on GitHub →](https://github.com/doremonn2847/IRS-project-analysis)
