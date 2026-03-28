We thank the reviewer for the comments. Below we respond to the weaknesses the reviewer listed.

1. ***Clarification on UCB (APUB) vs. VaR/CVaR*** (For weakness 1, )

These concepts address fundamentally different types of uncertainty and are not direct competitors:

* ***UCB (Epistemic)***: A frequentist tool for quantifying uncertainty due to ***data scarcity*** (estimation error).

* ***VaR/CVaR (Aleatoric)***: Risk measures for quantifying ***inherent randomness*** (tail risk) within a distribution.

In short, UCB manages exploration under limited samples, whereas VaR/CVaR manages risk-aversion for known distributions. Comparing them is a category error.


2. ***Importance of APUB*** (For weakness 1)
   
APUB considers the average of all outcomes worse than the standard Efron’s Bootstrap UCB threshold, analogous to how CVaR expands upon VaR. This approach applies the logic of risk-averaging to frequentist inference against epistemic uncertainty. APUB is more robust than Efron's UCB, accounting for the severity of the tail of the bootstrap distribution. Used in optimization, APUB can greatly simplifies the computation because it preserves the convexity of the original objective function.

3. ***APUB-M vs. DRO***

DRO specifies a gemerotic uncertainty set of distribution (Wasserstein ball with a radius $\epsilon$), which is not a statistical concept since $\epsilon$ is not related to the sample size $N$. Differently, APUB-M is a statiscal tool. While the both provide robustness, they offer different trade-offs in practice.  

Advantages of APUB-M:

* Data-Driven Convergence: When pistemic uncertainty vanishes as $N \to \infty$, APUB-M does not require manual parameter tuning to achieve asymptotic convergence. This is a UCB's foundamental property. DRO requires carefully scaling $\epsilon$ as a function of $N$.

* Parameter Transparency: The nominal level ($1-\alpha$) has a consistent probabilistic interpretation across applications, allowing to set a confidence level (e.g., $1 - \alpha$ = 95\%) without deep domain-specific calibration. DRO requires case-by-case calibration to avoid over-conservatism.

* Handling Random Recourse in Two-Stage Problems. As demonstrated in our numerical examples, APUB-M effectively handles two-stage stochastic programming with ***random recourse***. Traditional DRO often faces significant computational and theoretical hurdles in this setting, particularly regarding the dual reformulation of the inner maximization. APUB is a more flexible alternative for complex decision structures.

Limitations and Statistical Guarantees:

* As a frequentist statistical tool, APUB is primarily characterized by its asymptotic properties rather than finite-sample bounds. However, as proven in Proposition 2.4, APUB is first-order asymptotically correct. Specifically, the probability that the true mean is bounded by the APUB is at least $(1 - \alpha)$, with a convergence rate of $O(1/\sqrt{N})$.

* In a frequentist sense, the worst case should still be statistically plausible. While DRO can explore scenarios far beyond the support of the empirical data, APUB-M focuses on the reliability of the mean estimate within the observed distribution, leading to more actionable decisions.
