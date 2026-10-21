# Machine Unlearning

## Removal targets and guarantees

- **[Retraining as the reference](https://arxiv.org/abs/1907.05012)** (2019). Defines deletion relative to the learning algorithm trained on retained data. For randomized training, compare output distributions; matching the original model’s accuracy or making forgotten examples incorrect is a different target.

- **[Data removal versus behavior suppression](https://arxiv.org/abs/2412.06966)** (2024). Removing a training contribution, erasing a concept and preventing an output are different objectives. Retained data may teach the same fact; success at suppressing answers need not establish equivalence to retraining.

- **[Certified removal](https://proceedings.mlr.press/v119/guo20c.html)** (2020). Combines a Newton removal update with a randomly perturbed training objective. Bounds residual gradients to certify approximate retraining equivalence for regularized linear classifiers; convexity, smoothness and data bounds are part of the guarantee.

- **[Output versus full-state deletion](https://arxiv.org/abs/2007.02923)** (2020). Deletion can constrain only the published model or also retained optimizer state. Descent-to-Delete distinguishes these targets; hidden checkpoints and auxiliary state matter when later updates can expose them.

- **[Deletion capacity and generalization](https://arxiv.org/abs/2103.03279)** (2021). Studies how many deletions preserve population-risk guarantees under compute and storage constraints. Convex-loss results separate data-dependent unlearning from using DP alone; bounds depend on dimension and assumptions.

## Deletion-aware training and efficient retraining

- **[Summation-form unlearning](https://www.cs.columbia.edu/~junfeng/papers/unlearning/)** (2015). Cao and Yang express suitable learning procedures through maintained statistical sums. Removing a record updates those sums; applicability depends on the algorithm’s representation and includes upstream feature processing.

- **[Deletion-efficient k-means](https://arxiv.org/abs/1907.05012)** (2019). Ginart et al. use quantization and divide-and-conquer structures to reduce deletion work. Demonstrates that training can be designed around future removal; speedups concern those clustering algorithms and retained state.

- **[SISA](https://arxiv.org/abs/1912.03817)** (2019). Shards data, trains separate models and saves checkpoints across slices. A deletion retrains affected shards from earlier checkpoints; the reference is the SISA training procedure, not an ordinary monolithic model.

- **[Data removal-enabled forests](https://arxiv.org/abs/2009.05567)** (2020). Caches node statistics and selectively rebuilds affected subtrees. Exact deletion is defined relative to the DaRE forest learner; randomized upper splits trade some predictive flexibility for cheaper updates.

- **[DeltaGrad](https://arxiv.org/abs/2006.14755)** (2020). Reuses cached training trajectories and approximate gradient updates after small dataset changes. Accelerates retraining; numerical closeness to a retrained model should not be reported as a distributional removal certificate.

- **[Descent-to-Delete](https://arxiv.org/abs/2007.02923)** (2020). Uses convex optimization and reservoir sampling for long adversarial update sequences. Under its assumptions, per-deletion work and steady-state error need not grow with sequence length; guarantees differ for output and full-state removal.

- **[Exact unlearning through coupling](https://proceedings.mlr.press/v134/ullah21a.html)** (2021). Couples noisy-SGD trajectories to match the model/state law of retraining after deletion. Exactness extends beyond convex losses; stability controls reuse, while excess-risk bounds assume smooth convex problems.

- **[Adaptive deletion requests](https://arxiv.org/abs/2106.04378)** (2021). Requests chosen after inspecting published models violate independence assumptions used by some earlier guarantees. Gupta et al. construct an attack on SISA and a DP-based reduction for handling adaptive sequences.

## Post-hoc neural methods

- **[Weight scrubbing](https://arxiv.org/abs/1911.04933)** (2019). Uses approximations to how forgotten data affect trained weights, with noise to reduce remaining information. The theory and practical deep-network approximation must be separated; low forget-set accuracy alone does not validate scrubbing.

- **[SCRUB](https://arxiv.org/abs/2302.09880)** (2023). Uses a frozen teacher: encourages student disagreement on forget data while preserving agreement and predictive utility on retained data. Evaluates privacy, bias removal and mislabeled-data correction with distinct success criteria.

- **[Selective Synaptic Dampening](https://arxiv.org/abs/2308.07707)** (2023). Compares Fisher-based importance on training and forget sets, then damps disproportionately forget-important weights. Avoids retraining but needs importance statistics; empirical forgetting is not an exact-removal guarantee.

- **[Negative Preference Optimization](https://arxiv.org/abs/2404.05868)** (2024). Downweights forget-example gradients as their likelihood falls relative to a reference model, limiting continued ascent on already-suppressed examples. TOFU gains concern forgetting/utility tradeoffs, not certified removal.

- **[Representation Misdirection for Unlearning](https://arxiv.org/abs/2403.03218)** (2024). RMU redirects representations on selected forget data while preserving retain representations. Reduced hazardous-knowledge benchmark accuracy is a behavioral result; it does not establish removal of specific training records.

- **[Erasing diffusion concepts](https://arxiv.org/abs/2303.07345)** (2023). Fine-tunes a text-to-image model using negative guidance for a named concept. Changes generation behavior without identifying every relevant training image; concept suppression and exact dataset deletion remain different tasks.

## Benchmarks and comparative evidence

- **[TOFU](https://arxiv.org/abs/2401.06121)** (2024). Uses fictitious author profiles to create controlled forget and retain sets for LLMs. Original baselines fail to match desired forgetting and utility simultaneously; synthetic fine-tuning data make a retraining comparison feasible.

- **[MUSE](https://arxiv.org/abs/2407.06460)** (2024). Measures verbatim/knowledge memorization, privacy, retained utility, deletion scale and repeated requests. On tested 7B models, suppressing text did not ensure privacy or sustained utility across successive removals.

- **[NeurIPS unlearning competition](https://arxiv.org/abs/2406.09073)** (2024). Evaluates forgetting against distributions of retrained models while checking utility. Leading entries outperform tested baselines, but findings depend on the competition models, forget sets and compute-intensive evaluation protocol.

- **[Interclass Confusion test](https://arxiv.org/abs/2201.06640)** (2022). Adversarially alters training labels to make removal failures observable. Exposes weaknesses missed by ordinary forget-set metrics; the test probes a constructed training intervention rather than certifying all possible data removals.

- **[Per-example likelihood evaluation: RULI](https://arxiv.org/abs/2506.13009)** (2025). Uses inference attacks to assess removal efficacy and privacy against retraining. Finds failures hidden by aggregate evaluations; stronger attacks improve empirical evidence without proving absence of all leakage.

- **[Distinguishing unlearned from retrained models](https://arxiv.org/abs/2505.08138)** (2025). Mirror-model experiments distinguish tested unlearning outputs from retraining controls. The paper formalizes computational unlearning; its adversary-based target is stronger than agreement on a small set of utility metrics.

## Recovery attacks and sequential releases

- **[Eight tests of LLM unlearning](https://arxiv.org/abs/2402.16835)** (2024). Evaluates the “Who’s Harry Potter” model with extraction, question answering and representation probes. Familiarity scores suggest forgetting while other tests recover knowledge; conclusions concern that model and evaluation setting.

- **[Retain-only relearning](https://arxiv.org/abs/2505.22310)** (2025). In controlled vision experiments, fine-tuning only retained examples restores forget-set accuracy after several unlearning methods, but not after retraining. Tests persistence of removal, beyond immediate post-unlearning outputs.

- **[Before-and-after membership attacks](https://arxiv.org/abs/2005.02205)** (2020). Comparing model versions can reveal which records were deleted, sometimes more effectively than attacking the original model alone. An audit that exposes only the final model can miss leakage from the release history.

- **[Removal evaluation record](https://arxiv.org/abs/2407.06460)** (2024). Specify forget units, retained overlap, retraining algorithm, observable state, attacks, utility and repeated requests. Include preparation/storage costs; low forget-set accuracy is insufficient when retraining would still predict those examples.

## Related topics

[Privacy preserving learning](https://github.com/mlpapers/privacy-preserving-learning) · [Continual learning](https://github.com/mlpapers/continual-learning) · [Interpretability](https://github.com/mlpapers/interpretability) · [Evaluation](https://github.com/mlpapers/evaluation) · [Generative models](https://github.com/mlpapers/generative-models)
