We thank the reviewer for the comments. Below we respond to the weaknesses the reviewer listed.

1. ***Clarification on UCB (APUB) vs. VaR/CVaR*** (For weakness 1, )

These concepts address fundamentally different types of uncertainty and are not direct competitors:

UCB (epistemic uncertainty): A frequentist tool for quantifying uncertainty due to data scarcity (estimation error).

VaR/CVaR (aleatoric uncertainty): Risk measures for quantifying inherent randomness (tail risk) within a distribution.

In short, UCB manages exploration under limited samples, whereas VaR/CVaR manages risk-aversion for known/estimated distributions. Comparing them is a category error.


2. ***Importance of APUB*** (For weakness 1)
   
APUB considers the average of all outcomes worse than the standard Efron’s Bootstrap UCB threshold, analogous to how CVaR expands upon VaR. This approach applies the logic of risk-averaging to frequentist inference against epistemic uncertainty. APUB is more robust than Efron's UCB, accounting for the severity of the tail of the bootstrap distribution. Used in optimization, APUB can greatly simplifies the computation because it preserves the convexity of the original objective function.
