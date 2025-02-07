[View the code the generated this analysis (Python Juypter Notebooks)](https://github.com/ALILODHI-cloud/UVAmacro.github.io/blob/main/post_3/analysis.ipynb)

<head>
  <script type="text/javascript" async
    src="https://polyfill.io/v3/polyfill.min.js?features=es6">
  </script>
  <script type="text/javascript" async
    src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
  </script>
</head>


**Section 1: PCA Intro** 

Suppose we have the following, two-dimensional, data:


![Alt_text](figures/figure_1.jpg)

The orange arrows identify the most salient axes of variation in the data. In other words, most of the variance in our data is captured by the 'big X and Y - small X and Y'; the most common 'way' in which one observations differs from another, is by one having a large X and Y, and the other having a small X and Y. Then, clearly, the second most common 'way' is that one observation has a large X and small Y, whereas the other has a small X and large Y — this is described by the shorter arrow, which captures a smaller proportion of the variance than the longer arrow. Finally, note that the identified axes of variation are simply linear combinations of variables X and Y, where the sign of the weights on each variable reflect whether increases in that variable are associated with movements up, or down, the corresponding axis.  

Principal Component Analysis (PCA) leverages a technique called 'Eigenvalue Decomposition' to identify arrows like the orange ones – that is, the major axes of variation in a given set of data. Consider Figure 2, for instance, which gives the output of a PCA decomposition on yield level data. 'PC1', or the first 'principal component', is the axis that captures most of the variation in the data. Note that the weight, or 'loading', on each variable is positive, indicating that PC1 captures the variation that occurs due to some observations having across-the-board high yields, and others having across-the-board low yields. Thus we can term PC1 the 'level' component of our yield data. Looking next at PC2, we find that short and long-tenor yields are inversely-signed, indicating that this component has captured the variation ascribable to differences in the slope of the yield curve, across observations. Hence, PC2 is a 'slope' component. Similiar reasoning establishes that PC3 is most aptly described as a 'curvature' component. 

Figure 3 demonstrates the power of PC1, plotting that component against the ACM measure of 10yr term premia. The intuition behind why the two track so well, is that PC1 captures broad-based increases and decreases in yield levels; when PC1 is increasing, yields are, roughly speaking, rising across the board—and when it is falling, they are falling across the board. On the other hand, movements in yields can be decomposed into changes in policy (ffr) path pricing and term premia. Intuitively, broad-based increases are not typically driven by increases in policy-pricing, because, for example, if more tightening is being priced into the front and belly, then this should weigh on longer tenors. This leaves term premia as the driver, and hence explains why it tracks so well with PC1. Similiar reasoning establishes why decreases in PC2 implies compression in term premia.  



**Section 2: Linear regression + feature selection via mutual information** 

In this section, we retain a linear regression framework, but select regressors (‘features’) in a more algorithmic fashion. In particular, the feature utility metric ‘mutual information’ is deployed on a data set comprising 60 variables (figure 2). 

As a summary overview, given a prospective feature X and target Y, this technique computes a mutual information score according to:

$$
I(X; Y) = \sum_{x \in X} \sum_{y \in Y} p(x, y) \log \left( \frac{p(x, y)}{p(x) p(y)} \right)
$$

To gain some intuition, suppose X is a binary RV indicating whether a particular person used an umbrella on a given day. Suppose Y is a binary RV indicating whether it rained on a given day. 

Let our first observation be such that X=1, Y=1 (i.e. an umbrella was used and it rained). The summand resolves to 

$$
I(X; Y) = (\text{prop of obs in which X=1 and Y=1}) \times \log \left( \frac{(\text{prop of obs in which X=1 and Y=1})}{(\text{prop of obs in which X=1) (prop of obs in which Y=1)}} \right)
$$

Because "prop of odds in which X=1" and "prop of odds in which Y=1" will both, naturally, be _basically_ equal to "prop of odds in which X=1 AND Y=1", the argument in the log term will be greater than 1, and thus the log term itself greater than 0. Therefore observation one will contribute positively to the MI score. Also, because "prop of obs in which X=1 and Y=1" is quite large, the positive contribution will be weighted quite heavily. The result is a large MI score. 

We will also, however, have cases where, say, (X=1, Y=0). The summand would in this case be:

$$
I(X; Y) = (\text{prop of obs in which X=1 and Y=0}) \times \log \left( \frac{(\text{prop of obs in which X=1 and Y=0})}{(\text{prop of obs in which X=1) (prop of obs in which Y=0)}} \right)
$$

Intuitively, the numerator in the log term would be smaller than the denominator, and so the log would resolve to something less than zero. While this observation would thus detract from the MI score, it would do so in a way which is scaled by "prop of obs in which X=1 and Y=0" - which is to say, not by much ("prop of obs in which X=1 and Y=0" is likely very small).

Application of mutual information to our feature space produces the ranking displayed in Figure 2. It is notable that forward swap rates comprise the bulk of the highest-performing variables. 

![Alt_text](figures/figure_2.jpg)

**Section 3: Performance of the feature-selected model** 

When thinking about which variables to include as features in our model, we might consider starting with the top 10 (as ranked by MI), computing performance, then adding the next-best 10, computing performance, and so forth. When doing this, it is notable that the largest drop-offs in performance coincide with the largest drop-offs in MI score (Figure 3). This happens, presumably, because if a variable is uninformative about the 2s10s curve, then its inclusion is tantamount to forcing the model to learn a relationship which doesn't exist - that is, noise. 

![Alt_text](figures/figure_3.jpg)

In our case, inclusion of the **top 50** variables appears optimal. Thus our model is now:

$$\text{2s10s curve} = \beta_0 + \sum_{i=1}^{50} \beta_i \cdot X_{\text{feature with i-th highest MI score}}$$

This model sees vast improvements upon the simple model from earlier (Figure 4). 

![Alt_text](figures/figure_4.jpg)

**Conclusion**

Future extensions will entail translating this fair-value model into trading signals that can support a simple relative-value strategy. I will also attempt backtesting of some sort. 




