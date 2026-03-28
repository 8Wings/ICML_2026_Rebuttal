We thank the reviewer for the careful reading. Below we address the main concerns point by point.

**Weakness 1**

We respectfully disagree that APUB-M is a mere recombination of existing tools. The novelty of our work lies in the theoretical synthesis of risk-theoretic structures and frequentist inference:

* Conceptual Novelty: While CVaR is a measure of aleatoric risk, APUB-M repurposes that mathematical structure to quantify epistemic uncertainty. This is a foundational shift, not an incremental one. Like Efron’s Bootstrap, which uses quantile structures (VaR) for frequentist bounds, APUB-M provides a new, statistically consistent estimator for UCB.
* Theoretical vs. Empirical Superiority: The reviewer suggests that "incremental" work requires "exceptional empirical evidence." However, we provide theoretical guarantees (e.g., Prop 2.4) showing APUB-M achieves first-order asymptotic correctness—a property many heuristic "combinations" lack. In the field of ML theory, a method with proven statistical consistency and a $O(1/\\sqrt{N})$ rate offers a level of reliability that empirical results alone cannot provide.
* Unique Practical Capability: APUB-M’s primary "superiority" is its ability to handle random recourse in two-stage problems—a setting where traditional DRO faces significant computational and dual-reformulation hurdles. We focused our empirical evidence on this challenging, novel application specifically because existing "standard" methods struggle to operate there.

APUB-M is a mathematically distinct framework with unique convergence properties. Its value is not just in "practical performance," but in providing a theoretically grounded, tuning-free alternative to DRO for complex decision structures.

**Weakness 2, 3**

We clarify that the omission of DRO baselines was a deliberate choice based on the structural incompatibility of standard DRO with the random recourse problems studied. The distinction between APUB-M (statistical) and DRO (geometric) is fundamental and does not require numerical demonstration:

* Tractability in Random Recourse: Our paper focuses on two-stage stochastic programs with random recourse (where the recourse matrix $W$ is stochastic). In this setting, traditional Wasserstein DRO lacks a tractable dual reformulation for the inner maximization, often leading to NP-hard subproblems. APUB-M, being a statistical UCB, maintains computational tractability ($O(1/\\sqrt{N})$) without requiring these complex geometric reformulations.
* Statistical vs. Geometric Foundations: As shown in Prop 2.4, APUB-M is a data-driven statistical tool that achieves asymptotic correctness naturally as $N \to \infty$ (see the numerical studies). In contrast, DRO relies on a geometric uncertainty set (e.g., Wasserstein radius $\epsilon$) that requires manual, case-specific tuning of $\epsilon(N)$ to avoid extreme over-conservatism—a process that lacks the transparent probabilistic interpretation ($1-\alpha$) provided by APUB-M.
* Parameter Transparency: APUB-M uses a nominal confidence level $(1-\alpha)$ with a consistent probabilistic interpretation (e.g., 95%). DRO’s $\epsilon$ requires case-by-case calibration; determining a physically or statistically meaningful value for $\epsilon$ remains a significant challenge in DRO literature.
* Baseline Selection: We compared against SAA-M and the L-shaped method because they are the rigorous benchmarks for two-stage programs with random recourse. While DRO is effective for fix recourse problems, applying "SOTA Wasserstein DRO" to our specific random recourse setting is an open research challenge.






**2 “Could the authors explain the rationale behind limiting the empirical evaluation to a single two-stage product-mix problem?”**

**Response.** The rationale is that our algorithmic contribution is specifically designed for two-stage linear stochastic programs with random recourse, and the product-mix family is a representative benchmark for this problem class. At the same time, the empirical study is broader than a single fixed instance: it examines out-of-sample performance, empirical coverage, and computational behavior across multiple sample sizes, nominal levels, bootstrap sizes, and problem dimensions, with repeated randomly generated instances. We agree that additional benchmark families would strengthen the paper, and we will state this limitation more explicitly. However, we do not believe the current empirical study is too narrow to support the paper's core claims in the setting it explicitly targets.

**3 “Could the authors clarify why SOTA DRO baselines were excluded ...? How does APUB-M specifically outperform these modern surrogate models ...?”**

**Response.** We agree that broader comparisons would be valuable. In the current submission, classical DRO baselines were not included because the target setting involves *random recourse*, where such formulations are computationally much harder to handle. Our paper therefore does *not* claim universal empirical superiority over all modern DRO methods. Rather, it proposes a complementary robustness framework: APUB-M directly robustifies the estimator through a statistically interpretable nominal level, instead of introducing an ambiguity set and radius. Empirically, what we show is that APUB-M substantially improves out-of-sample reliability relative to SAA-M in the small-data regime while remaining computationally tractable. Since SAA-M is the $(1-\alpha)=0$ special case of APUB-M, this comparison also isolates the effect of the proposed upper-confidence correction itself.

**4 “Regarding the synthetic data generation ... the mixture of normal and worst-case scenarios raises a concern about potential empirical bias...”**

**Response.** We would like to clarify the intent of the data-generating process. The numerical study uses a stylized two-regime synthetic generator to represent regular periods together with rare adverse periods. The purpose is not to artificially exaggerate tail risk, but to test the scenario that motivates the paper: under limited data, rare but decision-relevant regimes may be poorly captured by standard plug-in approaches. Since both APUB-M and SAA-M are evaluated under the same generator, the setup does not mechanically favor our method; rather, it provides a controlled stress test for epistemic robustness. We agree that additional sensitivity analysis and more benchmark settings would further strengthen the empirical section.

**5 “To ensure reproducibility ... will the authors make their code and data publicly available?”**

**Response.** We agree that reproducibility is important. Since the experiments use synthetic rather than proprietary data, the main reproducibility artifacts are the instance generator, optimization code, and evaluation scripts. Subject to the venue's anonymization and artifact policies, we plan to make these materials publicly available. We will also improve the reproducibility discussion in the revision.

**6 “Addressing the above empirical limitations will be crucial for establishing the true generality of the APUB-M framework...”**

**Response.** We agree that extending APUB-M to broader benchmark families and to settings such as nonlinear or multi-stage stochastic optimization would be valuable future work. At the same time, we do not believe that these natural extensions diminish the present contribution. The current paper already makes a substantive advance in a clearly defined and technically challenging setting: it introduces a new epistemic-robust objective, establishes its core asymptotic properties, and develops a practical algorithmic framework for solving it in two-stage random-recourse models.

Overall, we appreciate the reviewer's concerns and agree that broader empirical validation would further strengthen the paper. However, we respectfully believe the current work already makes a nontrivial statistical, theoretical, and algorithmic contribution in its stated scope.


