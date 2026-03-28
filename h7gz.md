We thank the reviewer for the careful reading and constructive feedback. We also appreciate the recognition of the paper's theoretical clarity and algorithmic efficiency. Below we address the main concerns point by point.

**(1) “The proposed APUB-M framework is fundamentally an incremental contribution...”**

**Response.** We respectfully disagree with this characterization. Our contribution is not simply a recombination of bootstrap and CVaR-like ideas. The paper introduces APUB as a new optimization-oriented statistical object, proves its asymptotic correctness and consistency, and develops a practical algorithmic framework for solving the resulting models in two-stage stochastic programs with random recourse. Importantly, APUB is *not* CVaR of the realized random cost; it is a CVaR-type functional of the *bootstrap sampling distribution of the sample mean*. Hence it targets *epistemic uncertainty* in the estimator rather than aleatoric tail risk in the underlying system. We will revise the manuscript to make this distinction even more explicit.

**(2) “Could the authors explain the rationale behind limiting the empirical evaluation to a single two-stage product-mix problem?”**

**Response.** The rationale is that our algorithmic contribution is specifically designed for two-stage linear stochastic programs with random recourse, and the product-mix family is a representative benchmark for this problem class. At the same time, the empirical study is broader than a single fixed instance: it examines out-of-sample performance, empirical coverage, and computational behavior across multiple sample sizes, nominal levels, bootstrap sizes, and problem dimensions, with repeated randomly generated instances. We agree that additional benchmark families would strengthen the paper, and we will state this limitation more explicitly. However, we do not believe the current empirical study is too narrow to support the paper's core claims in the setting it explicitly targets.

**(3) “Could the authors clarify why SOTA DRO baselines were excluded ...? How does APUB-M specifically outperform these modern surrogate models ...?”**

**Response.** We agree that broader comparisons would be valuable. In the current submission, classical DRO baselines were not included because the target setting involves *random recourse*, where such formulations are computationally much harder to handle. Our paper therefore does *not* claim universal empirical superiority over all modern DRO methods. Rather, it proposes a complementary robustness framework: APUB-M directly robustifies the estimator through a statistically interpretable nominal level, instead of introducing an ambiguity set and radius. Empirically, what we show is that APUB-M substantially improves out-of-sample reliability relative to SAA-M in the small-data regime while remaining computationally tractable. Since SAA-M is the $(1-\alpha)=0$ special case of APUB-M, this comparison also isolates the effect of the proposed upper-confidence correction itself.

**(4) “Regarding the synthetic data generation ... the mixture of normal and worst-case scenarios raises a concern about potential empirical bias...”**

**Response.** We would like to clarify the intent of the data-generating process. The numerical study uses a stylized two-regime synthetic generator to represent regular periods together with rare adverse periods. The purpose is not to artificially exaggerate tail risk, but to test the scenario that motivates the paper: under limited data, rare but decision-relevant regimes may be poorly captured by standard plug-in approaches. Since both APUB-M and SAA-M are evaluated under the same generator, the setup does not mechanically favor our method; rather, it provides a controlled stress test for epistemic robustness. We agree that additional sensitivity analysis and more benchmark settings would further strengthen the empirical section.

**(5) “To ensure reproducibility ... will the authors make their code and data publicly available?”**

**Response.** We agree that reproducibility is important. Since the experiments use synthetic rather than proprietary data, the main reproducibility artifacts are the instance generator, optimization code, and evaluation scripts. Subject to the venue's anonymization and artifact policies, we plan to make these materials publicly available. We will also improve the reproducibility discussion in the revision.

**(6) “Addressing the above empirical limitations will be crucial for establishing the true generality of the APUB-M framework...”**

**Response.** We agree that extending APUB-M to broader benchmark families and to settings such as nonlinear or multi-stage stochastic optimization would be valuable future work. At the same time, we do not believe that these natural extensions diminish the present contribution. The current paper already makes a substantive advance in a clearly defined and technically challenging setting: it introduces a new epistemic-robust objective, establishes its core asymptotic properties, and develops a practical algorithmic framework for solving it in two-stage random-recourse models.

Overall, we appreciate the reviewer's concerns and agree that broader empirical validation would further strengthen the paper. However, we respectfully believe the current work already makes a nontrivial statistical, theoretical, and algorithmic contribution in its stated scope.


