# Aidan Riordan — posters, papers, talks

PhD student in Industrial Engineering, Northeastern University (operations research: simulation-optimization
of pharmaceutical supply chains under drug shortages). Contact: riordan.a@northeastern.edu

## Papers

### [Large Language Models for Metaheuristic Implementation: A Case Study with Variable Neighborhood Search](https://link.springer.com/chapter/10.1007/978-3-032-19582-1_11)
*Springer Lecture Notes in Computer Science, 2025 — first author*

Metaheuristics are widely used in combinatorial optimization but take real expertise and engineering effort
to implement. We ask whether current LLMs can turn a state-of-the-art algorithm description into performant
code with minimal human intervention. We introduce a generalizable prompting framework — Context,
Communication, Iteration (CCI) — and use it to replicate a Variable Neighborhood Search for the balanced
minimum sum-of-squares clustering problem with Gemini 2.5 Pro and Claude Sonnet 4. Gemini's implementation
came within 0.032% of the reference on average (median 0.009%), statistically non-inferior within a 0.01%
margin, and it corrected a missing term in the neighborhood-evaluation formula as printed in the source
paper; Claude did not. LLM-assisted engineering looks like a viable path to making high-performance
methods accessible to more researchers. An extended version is under review at the *Journal of Heuristics*.

### [Interpretability, Adaptability and Scalability of Variable Neighborhood Search](https://link.springer.com/chapter/10.1007/978-3-031-62912-9_30)
*Springer Lecture Notes in Computer Science, June 2024 — 15th Metaheuristics International Conference (MIC 2024), Lorient, France — co-author with Pierre Hansen and Xavier Hansen; presenter*

Twenty-five years on, Variable Neighborhood Search remains an effective and accessible metaheuristic. The
paper argues that its way of escaping local optima gives it three properties that suit large, complex
real-world problems: interpretability (a simple modular design that invites problem analysis and systematic
formulation of the search space), adaptability (it hybridizes naturally with other methods) and scalability
(it parallelizes and integrates AI/ML components readily). It closes with recommendations for the community:
public code repositories and problem libraries, documented real-world implementations, engagement across
metaheuristics, and popularizing VNS as an accessible technique.

### [The Jessamine Symbolic Regression System and a Reliability Approach to Benchmarking](2026-jessamine-symbolic-regression-reliability-preprint.pdf)
*Preprint, under review at Evolutionary Computation (MIT Press) — W. Garrett Mitchener, Aiden Camilleri, Aidan Riordan, Latherial Calbert — co-author*

Symbolic regression searches for a prediction function in exact algebraic form, so the model is readable
rather than a black box. Jessamine is an open-source evolutionary symbolic-regression system in Julia
([Jessamine.jl](https://github.com/wgm-applied-math/Jessamine.jl)). Instead of evolving expression trees,
each genome is a flat list of instructions that computes a set of derived features, and the prediction is a
linear combination of those features. The paper tests it on SRBench and cp3-bench data sets and argues that
symbolic-regression benchmarks should report how *reliably* an algorithm recovers the true equation, not
only its best run. This is a preprint and has not yet been peer reviewed.

**Contributions**

- **Flat-genome architecture with three layers of optimization.** Ridge regression fits the linear weights,
  Nelder–Mead fits the scalar parameters, and an evolutionary search works on the feature functions. Because
  the model is a sum of terms, a genome that finds one correct term already scores better. Recombination can
  then merge correct terms found by different individuals into one child.
- **A reliability metric for stochastic algorithms.** Each data set gets 32 independent 15-minute runs
  (8 core-hours in total). A Beta posterior over the per-run success rate then gives a 95% credible lower
  bound on the probability that an 8-hour run recovers the ground-truth equation. The paper proposes this
  as a reporting standard.
- **Evidence that mistuned hyper-parameters explain weak benchmark results.** Many benchmarks tune on noisy
  data and test on noise-free data, or the reverse. On a noisy sin(x) data set, raising the complexity
  penalty from 1e-12 to 1e-2 turns overfit results into 31 of 32 runs that recover sin(x).
- **Strong ground-truth recovery.** Jessamine recovers 13 of the 14 Strogatz ODE targets, some of them
  only with low reliability. The remaining target becomes reliable once cot is added to the operator set.
  It recovers the Friedman f1 function, including from data with irrelevant distractor columns. It recovers
  5 of the 8 cp3-bench F functions with very high reliability, while no algorithm in the original cp3-bench
  study recovered more than four. On several black-box cosmology data sets its error is lower than the best
  previously reported. One example is C3b, at 3.9e-14 compared with 3.6e-11.
- **A vocabulary for why symbolic regression fails.** *Series traps* (settling on a Taylor-series
  approximation), *cruft traps* (overly complicated but accurate expressions) and the *partial-credit
  problem* (products such as 0.3x·sin 2x, where neither factor alone fits the data). The paper ends with
  concrete recommendations for designing benchmark data sets.

## Posters

### [Why Can Large Language Models Optimize?](2025-optimization-days-llm-metaheuristic-poster.pdf)
*Optimization Days 2025, Montréal · NSF NRT poster session, Northeastern — first author, presenter*

The poster version of the LLM-replication study above: give the model only the paper describing a VNS
algorithm (the original code was never released) and ask for code that matches the original's performance.
It shows the CCI prompting framework, the benchmark against the reference implementation, where the models
fail, and what that says about LLMs as research assistants for metaheuristics.

### [Evolutionary algorithm for inferring differential equations](2025-dynamics-days-evolutionary-diffeq-poster.pdf)
*Dynamics Days 2025 — with W. Garrett Mitchener (College of Charleston) — co-author*

Symbolic regression that recovers the governing equations of a physical system from sampled data. Jessamine
is a flexible evolutionary framework in which each candidate model is a linear combination of evolved
functions, fitted in three layers: ridge regression for the linear weights, a general minimizer for scalar
parameters, and an evolutionary search over the functions themselves (with variable-neighborhood-style
escapes when innovation stalls). As a test case it recovers the Brusselator reaction–diffusion PDEs exactly
from synthesized samples of the fields and their spatial derivatives. Code: [Jessamine.jl](https://github.com/wgm-applied-math/Jessamine.jl).

### [An Interpretable Machine Learning Method in Symbolic Regression — Jessamine](2024-surf-interpretable-ml-jessamine-poster.pdf)
*College of Charleston SURF (Summer Undergraduate Research) grant, 2024 — advisor W. Garrett Mitchener — author, presenter*

Black-box models are used for high-stakes decisions in healthcare and criminal justice, where a prediction
without a readable reason is a liability. This project asks whether an interpretable model can keep up.
Jessamine is a genetic-algorithm symbolic-regression system: each genome is a candidate function, populations
are mutated and recombined, the best are simplified into short algebraic expressions. Two results on the
poster: Jessamine's evolved features let XGBoost capture non-linear structure with a far simpler ensemble
than it needs on raw inputs, and on a 303-patient heart-disease dataset it surfaces the three predictors a
cardiologist would expect (ST depression, maximum heart rate, exercise-induced angina) while stating
honestly where its accuracy still trails black-box models.

Posters are the versions presented at the venues listed.
