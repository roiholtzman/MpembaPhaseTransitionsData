# Research validation protocol and audit

**Audit date:** 2026-10-29  
**Overall audit severity:** medium

## Validation rule

Before calling a computational result a scientific verification, trace the information flow from primitive inputs to the reported observable. Different files, seeds, solvers, or languages are not independent if they share the critical answer, reduction, implementation, reference, or adaptive selection step.

Use these terms strictly:

- **analytic prediction only** — no independent computation;
- **consistency check** — the prediction/equivalent quantity is inserted;
- **independent defining-formula check** — a more primitive exact formula is evaluated without inserting the claimed result;
- **independent dynamics/inference solve** — the parent ODE/PDE/SDE/inference problem is solved without inserting the answer;
- **cross-method replication at [layer]** — genuinely different methods agree at a named layer;
- **end-to-end validation** — the check starts upstream of the critical reduction and tests the actual parent object;
- **oracle/post-hoc diagnostic** — forbidden target/teacher information influenced method/protocol choice;
- **reference-informed evaluation** — target knowledge fixes an evaluation location/protocol;
- **conditional MC uncertainty** — sampling uncertainty with data/model/reference choices fixed;
- **finite-width evidence** / **scaling-consistent** — finite-size evidence without an established infinite-size result.

## Required validation card

For each consequential numerical check record:

- CLAIM_UNDER_TEST
- TARGET_LAYER
- PRIMITIVE_INPUTS
- THEORY_HARDCODED_IN_SOLVER
- UPSTREAM_SHARED_ASSUMPTIONS
- END_TO_END
- NUMERICAL_OBSERVABLE
- FALSIFICATION_CRITERION
- CONVERGENCE_PARAMETERS
- TRUE_INDEPENDENT_STATISTICAL_UNIT
- UNCERTAINTY_INCLUDED
- UNCERTAINTY_OMITTED
- ORACLE_OR_TARGET_INFORMATION_USED
- POST_SELECTION_OR_ADAPTIVITY
- VERIFICATION_STATUS

Also check train/tune/test reuse, post-selection, pseudoreplication, MCMC autocorrelation/ESS, paired randomness, shared implementation, numerical refinement, approximation-layer changes, fit-window selection, and reference uncertainty.

## Repository-specific audit findings

1. The repository contains summary CSVs of system size N and the mean/variance of transition time, but not raw realizations, generation code, seeds, or sample counts.
2. The number of N values is not the number of independent stochastic replications. Without replicate counts/raw data, sampling uncertainty on the reported mean/variance cannot be reconstructed here.
3. These CSVs are companion evidence for the paper, not an independent validation of the paper's simulation implementation.
4. A trend across finite N is **finite-width evidence** unless paired with the analytic thermodynamic argument or a controlled extrapolation.

## Validation card for the central current/legacy check

- **CLAIM_UNDER_TEST:** transition-time mean/variance has the reported N dependence.
- **TARGET_LAYER:** finite-N stochastic simulation summaries.
- **PRIMITIVE_INPUTS:** absent generator; CSV summaries only.
- **THEORY_HARDCODED_IN_SOLVER:** unknown from this repository.
- **UPSTREAM_SHARED_ASSUMPTIONS:** same generator/definitions as the paper.
- **END_TO_END:** no.
- **NUMERICAL_OBSERVABLE:** tabulated mean and variance versus N.
- **FALSIFICATION_CRITERION:** independent regeneration disagrees beyond sampling error.
- **CONVERGENCE_PARAMETERS:** N, replicate count, simulation timestep/mixing as applicable.
- **TRUE_INDEPENDENT_STATISTICAL_UNIT:** individual stochastic realization, not CSV rows.
- **UNCERTAINTY_INCLUDED:** variance column describes the simulated random variable, not automatically standard error of the mean.
- **UNCERTAINTY_OMITTED:** uncertainty of mean/variance estimates because replicate counts are absent.
- **ORACLE_OR_TARGET_INFORMATION_USED:** unknown.
- **POST_SELECTION_OR_ADAPTIVITY:** unknown.
- **VERIFICATION_STATUS:** archival finite-width summary evidence.

## Highest-value next independent check

Add or link the exact generator version and number of realizations per N; ideally archive raw/sufficient-statistic counts so standard errors can be reconstructed.

Preserve historical outputs and adaptive history. A new safeguard does not retroactively make an old run prospective or independent.
