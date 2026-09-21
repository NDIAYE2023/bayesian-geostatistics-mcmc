# Bayesian Geostatistics and MCMC for Latent Spatial Models

## Overview

This project was developed during my Master's end-of-studies internship at
**MIAT – INRAE Toulouse**.

The objective was to study Monte Carlo methods for Bayesian inference in
high-dimensional latent spatial models, with a particular focus on the
**Metropolis-Adjusted Langevin Algorithm (MALA)**.

The project investigates strategies for improving the efficiency and
robustness of MCMC sampling through:

- adaptive step-size selection,
- preconditioning,
- momentum persistence,
- sparse spatial approximations based on the Vecchia approach.

The methodology was first validated on a Gaussian spatial model and then
extended to non-Gaussian observation models.

---

## Research Problem

Let `w` denote a latent spatial Gaussian field observed indirectly through
data `y`.

The objective is to sample from the posterior distribution:

p(w | y)

For Gaussian observation models, the posterior distribution can be derived
analytically and therefore provides a reference case for validating MCMC
algorithms.

For non-Gaussian observation models, the posterior distribution is no longer
available in closed form and numerical sampling methods are required.

---

## MALA

The Metropolis-Adjusted Langevin Algorithm combines information from the
gradient of the log-posterior with a stochastic perturbation to construct
efficient MCMC proposals.

A Metropolis-Hastings correction ensures that the Markov chain targets the
desired posterior distribution.

Several variants of MALA were investigated in this project.

---

## Adaptive Step Size

The proposal step size strongly influences the efficiency of MALA.

An automatic adaptation procedure was implemented during the burn-in phase
to adjust the proposal scale toward a target acceptance rate.

After burn-in, the step size is fixed for posterior sampling.

---

## Preconditioning

Preconditioning was investigated to account for the geometry and dependence
structure of the latent spatial field.

The implementation relies on sparse matrix operations and Cholesky
factorizations rather than explicitly computing large matrix inverses.

The objective is to improve mixing and increase the effective sample size
of the MCMC chains.

---

## Vecchia Approximation

Gaussian spatial models become computationally expensive when the number
of spatial locations increases.

The **Vecchia approximation** replaces conditioning on all previous
observations by conditioning on small sets of neighboring observations.

This produces sparse precision structures and reduces computational and
memory requirements.

---

## Models

The repository contains implementations and experiments for several
observation models.

### Gaussian Model

The Gaussian model provides a reference case because its posterior
distribution can be computed analytically.

It was used to validate the MCMC implementation and compare different
sampling strategies.

### Binary Model

Binary observations are modeled using a Bernoulli distribution with a
logistic link and a latent Gaussian spatial field.

Since the posterior distribution is non-Gaussian, MCMC sampling is required.

A MAP estimate and local Hessian information can be used to construct
posterior-informed preconditioners.

### Poisson Model

The methodology was also extended to count data through a Poisson
observation model.

### Tobit Model

Additional experiments investigate a Tobit observation model for censored
data.

---

## Experimental Evaluation

Different MCMC configurations were compared through simulation experiments.

The analysis focuses on quantities such as:

- Effective Sample Size (ESS)
- Monte Carlo estimation error
- Acceptance rate
- Root Mean Squared Error (RMSE)
- Computational cost
- Robustness across model configurations

---

## Repository Contents

```text
bayesian-geostatistics-mcmc/
│
├── MALA_gaussien_dim1_dim2.qmd
├── MALA_binaire.qmd
├── MALA_poisson.qmd
├── MALA_Tobit.qmd
└── README.md
