We thank the reviewer for the careful reading. Below we address the main concerns point by point (***W: Weakness; Q: Question***).


**W1:**

We respectfully disagree that APUB-M is a mere recombination of existing tools. The novelty of our work lies in the theoretical synthesis of risk-theoretic structures and frequentist inference:

* Conceptual Novelty: While CVaR is a measure of aleatoric risk, APUB-M repurposes that mathematical structure to quantify epistemic uncertainty. This is a foundational shift, not an incremental one. Like Efron’s Bootstrap, which uses quantile structures (VaR) for frequentist bounds, APUB-M provides a new, statistically consistent estimator for UCB.
* Theoretical vs. Empirical Superiority: The reviewer suggests that "incremental" work requires "exceptional empirical evidence." However, we provide theoretical guarantees (e.g., Prop 2.4) showing APUB-M achieves first-order asymptotic correctness—a property many heuristic "combinations" lack. In the field of ML theory, a method with proven statistical consistency and a $O(1/\\sqrt{N})$ rate offers a level of reliability that empirical results alone cannot provide.
* Unique Practical Capability: APUB-M’s primary "superiority" is its ability to handle random recourse in two-stage problems—a setting where traditional DRO faces significant computational and dual-reformulation hurdles. We focused our empirical evidence on this challenging, novel application specifically because existing "standard" methods struggle to operate there.

APUB-M is a mathematically distinct framework with unique convergence properties. Its value is not just in "practical performance," but in providing a theoretically grounded, tuning-free alternative to DRO for complex decision structures.


**W2, W3, Q1:**

We clarify that the omission of DRO baselines was a deliberate choice based on the structural incompatibility of standard DRO with the random recourse problems studied. The distinction between APUB-M (statistical) and DRO (geometric) is fundamental and does not require numerical demonstration:

* Tractability in Random Recourse: Our paper focuses on two-stage stochastic programs with random recourse (where the recourse matrix $W$ is stochastic). In this setting, traditional Wasserstein DRO lacks a tractable dual reformulation for the inner maximization, often leading to NP-hard subproblems. APUB-M, being a statistical UCB, maintains computational tractability ($O(1/\\sqrt{N})$) without requiring these complex geometric reformulations.
* Statistical vs. Geometric Foundations: As shown in Prop 2.4, APUB-M is a data-driven statistical tool that achieves asymptotic correctness naturally as $N \to \infty$ regardless of $\alpha$ (see the numerical studies). In contrast, DRO relies on a geometric uncertainty set (e.g., Wasserstein radius $\epsilon$) that requires manual, case-specific tuning of $\epsilon(N)$ to avoid extreme over-conservatism—a process that lacks the transparent probabilistic interpretation ($1-\alpha$) provided by APUB-M.
* Parameter Transparency: APUB-M uses a nominal confidence level $(1-\alpha)$ with a consistent probabilistic interpretation (e.g., 95%). DRO’s $\epsilon$ requires case-by-case calibration; determining a physically or statistically meaningful value for $\epsilon$ remains a significant challenge in DRO literature.
* Baseline Selection: We compared against SAA-M and the L-shaped method because they are the rigorous benchmarks for two-stage programs with random recourse. While DRO is effective for fix recourse problems, applying "SOTA Wasserstein DRO" to our specific random recourse setting is an open research challenge. 


**Q2:**

We clarify that APUB-M "outperforms" modern surrogate models and DRO not necessarily by achieving the lowest point-estimate error, but through guaranteed statistical reliability and parameter transparency:

* Reliability vs. Precision: Modern surrogate models (e.g., GP or NN) focus on minimizing mean squared error but often provide poorly calibrated uncertainty bounds. APUB-M is specifically designed to be a UCB. As proven in Prop 2.4, it ensures that the true mean is bounded by the APUB with at least probability $(1-\alpha)$ asymptotically.
* Out of Sample (OOS) Coverage: In OOS testing, "superiority" for a UCB means the empirical mean of the OOS data rarely exceeds the APUB. While DRO can achieve this by choosing a very large $\epsilon$, it often results in over-conservatism that renders the decision useless. APUB-M provides a tighter, data-driven bound that scales naturally with $N$, avoiding the arbitrary "padding" typical of surrogate-based or geometric approaches.
* Avoidance of Overfitting: Surrogate models are prone to overfitting the training distribution, leading to overconfident (narrow) bounds that fail OOS. APUB-M inherits the robustness of frequentist averaging, making it structurally more resilient to the "optimizer's curse" where the decision-maker over-optimizes on a specific sample.
* Tuning-Free Consistency: Unlike surrogate models that require hyperparameter tuning (e.g., kernel choice, learning rates) or DRO which requires $\epsilon$-calibration, APUB-M is tuning-free. Its OOS performance is consistently tied to the chosen confidence level $(1-\alpha)$, providing a predictable and interpretable performance guarantee across different datasets.

APUB-M outperforms modern alternatives by providing a statistically principled way to balance performance and risk without the manual calibration or over-conservatism inherent in geometric DRO or surrogate-based heuristics.


**Q4:**

We clarify that our data-generating process is a deliberate stress test designed to evaluate robustness under distributional shifts, a standard practice in robust optimization and ML:

* purpose of the Two-Regime Model: The mixture of normal and worst-case scenarios is a stylized representation of regime-switching environments (e.g., financial crashes or supply chain disruptions). The goal is not to exaggerate tail risk, but to evaluate how estimators perform when the training sample is dominated by the normal regime while the testing environment includes rare, high-impact events.
* Fair Comparison: Crucially, both APUB-M and the baseline SAA-M are evaluated on the exact same data. The setup does not mechanically favor APUB-M; rather, it highlights that SAA-M (the "plug-in" approach) fails to account for the epistemic uncertainty of these hidden regimes, whereas APUB-M provides the necessary statistical coverage.
* Real-World Fidelity: Real-world data in high-stakes domains (healthcare, energy, finance) is rarely i.i.d. and often contains "black swan" events. Our generator mimics this heterogeneity. A model that performs well only on typical i.i.d. Gaussian data is precisely what leads to catastrophic failures in practice—the very problem APUB-M is designed to solve.
* Empirical Integrity: To ensure no artificial inflation of results, we can include a sensitivity analysis in the final version varying the mixing probability of the extreme regime to demonstrate that APUB-M remains reliable even as the frequency of tail events diminishes.


**Q5:**

We are committed to the reproducibility of our results. All code—including the APUB-M implementation, data generation scripts, and benchmarking suites—is already organized in a repository. We will release the full source code and datasets under an open-source license (e.g., MIT/Apache) immediately upon publication to allow the community to verify our computational claims and extend our work to other domains.


**Limitation:**

We thank the reviewer for identifying these high-value directions for future research. As the first work to introduce APUB, our priority was establishing foundational properties and efficacy in challenging settings like random recourse. We agree that extending APUB-M to non-linear or multi-stage optimization problems is a logical next step.


