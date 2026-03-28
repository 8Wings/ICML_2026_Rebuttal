We thank the reviewer for the comments. Below we respond to the weaknesses the reviewer listed.

1. ***Clarification on UCB (APUB) vs. VaR/CVaR*** (For weakness 1, )

These concepts address fundamentally different types of uncertainty and are not direct competitors:

* ***UCB (Epistemic)***: A frequentist tool for quantifying uncertainty due to ***data scarcity*** (estimation error).

* ***VaR/CVaR (Aleatoric)***: Risk measures for quantifying ***inherent randomness*** (tail risk) within a distribution.

In short, UCB manages exploration under limited samples, whereas VaR/CVaR manages risk-aversion for known distributions. Comparing them is a category error.


2. ***Importance of APUB*** (For weakness 1)
   
APUB considers the average of all outcomes worse than the standard Efron’s Bootstrap UCB threshold, analogous to how CVaR expands upon VaR. This approach applies the logic of risk-averaging to frequentist inference against epistemic uncertainty. APUB is more robust than Efron's UCB, accounting for the severity of the tail of the bootstrap distribution. Used in optimization, APUB can greatly simplifies the computation because it preserves the convexity of the original objective function.

3. ***APUB-M vs. DRO***

The distinction between APUB-M (statistical) and DRO (geometric) is fundamental and does not require numerical demonstration:

* Statistical vs. Geometric: DRO uses a geometric uncertainty set (e.g., Wasserstein ball with a radius $\epsilon$) where $\epsilon$ is often decoupled from sample size $N$. APUB-M is a data-driven statistical tool where the "uncertainty set" naturally scales with $N$.
* Parameter Transparency: APUB-M uses a nominal confidence level ($1-\alpha$) with a consistent probabilistic interpretation (e.g., 95%). DRO requires case-by-case calibration of $\epsilon$ to avoid over-conservatism or under-coverage.
* Asymptotic Convergence: APUB-M inherits UCB’s fundamental property: it converges as $N \to \infty$ without manual parameter decay. DRO requires specific $\epsilon(N)$ scaling laws to achieve similar consistency.
* Handling Random Recourse: APUB-M remains computationally tractable in two-stage stochastic programs with random recourse. In contrast, DRO often faces significant hurdles regarding dual reformulations of the inner maximization in these complex structures.
* Statistical Correctness: Per Prop 2.4, APUB is first-order asymptotically correct. The probability that the true mean is bounded by APUB is at least $1-\alpha$, with a convergence rate of $O(1/\sqrt{N})$.

Given these structural differences, APUB-M serves as a more transparent and statistically grounded alternative to DRO for complex decision structures. We will clarify these theoretical trade-offs in the final manuscript.



