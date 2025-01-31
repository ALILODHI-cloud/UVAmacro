[View work in progress at the following Jupyer Notebook](https://github.com/ALILODHI-cloud/UVAmacro.github.io/blob/main/post_3/analysis.ipynb)



In prior posts we have assumed the following structure for fair-value analysis of the 2s10s curve: linear regression of that curve on the 1y1y ois rate, 5y5y breakevens and size of the fed’s balance sheet as a share of US GDP. In this post, we will evaluate the out-of-sample performance of that model, and then attempt to improve upon it using feature-selection techniques borrowed from machine learning. 

**Section 1: Simple model performance** 

The simple model specification is as follows:

$$\text{2s10s curve} = \beta_0 + \beta_1 \times \text{1y1y OIS rate} + \beta_2 \times \text{5y5y breakeven rate} + \beta_3 \times \text{fed balance sheet as prop of US economy}$$

Having fit\trained this model on the 2006 start-2014 start sample, Figure 1 displays its performance on the 2014 - 2016 sample. Performance, as can be seen, is very poor. 

![Alt_text](figures/figure_1.jpg)


**Section 2: Linear regression + feature selection via mutual information** 

In this section, we retain a linear regression framework, but select regressors (‘features’) in a more algorithmic fashion. In particular, the feature utility metric ‘mutual information’ is deployed on a data set comprising 60 variables (figure 2). 

As a summary overview, given a prospective feature X and target Y, this techniques computes a mutual information score according to:

$$
I(X; Y) = \sum_{x \in X} \sum_{y \in Y} p(x, y) \log \left( \frac{p(x, y)}{p(x) p(y)} \right)
$$

To gain some intuition, suppose X is a binary RV indicating whether a particular person used an umbrella on a given day. Suppose Y is a binary RV indicating whether it rained on a given day. 

Suppose our first observation is such that X=1, Y=1 (i.e. an umbrella was used and it rained). The summand resolves to 

$$
I(X; Y) = (\text{prop of obs in which X=1 and Y=1}) \times \log \left( \frac{(\text{prop of obs in which X=1 and Y=1})}{(\text{prop of obs in which X=1) (prop of obs in which y=1)}} \right)
$$

Because "prop of odds in which X=1" and "prop of odds in which Y=1" will both, naturally, be _basically_ equal to "prop of odds in which X=1 AND Y=1", the argument in the log term will be greater than 1, and thus the log term itself greater than 0. Thus observation one in the data will contribute positively to the MI score. Also, because "prop of obs in which X=1 and Y=1" is quite large, this positive contribution will be weighted quite heavily. The result is a large MI score. 

We will also, however, have cases where, say, (X=1, Y=0). The summand would in this case be:

$$
I(X; Y) = (\text{prop of obs in which X=1 and Y=0}) \times \log \left( \frac{(\text{prop of obs in which X=1 and Y=0})}{(\text{prop of obs in which X=1) (prop of obs in which y=0)}} \right)
$$

Intuitively, the numerator in the log term would be smaller than the denominator, and so the log would resolve to something less than zero. While this observation would thus detract from the MI score, it would do so in a way which is scaled by "prop of obs in which X=1 and Y=0" - which is to say, not by much ("prop of obs in which X=1 and Y=0" is likely very small).

