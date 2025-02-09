[View the code that generated this analysis (Python Juypter Notebooks)](https://github.com/ALILODHI-cloud/UVAmacro.github.io/blob/main/post_1/analysis.ipynb)


# Section 1: Fair value analysis of the 2s10s curve 

In this note we consider a regression of the 2s/10s treasury curve on the 1y1y swap rate, 5y5y breakeven rate and BoFAML MOVE Index. The sample period runs from 2018-07-12 to 2024-11-27. 

### Swap rates and the macro narrative: 2024 in retrospect

Figure 1 encapsulates the narrative volatility that has characterized this year: an OER-driven reflationary narrative at the beginning; followed by a streak of soft-landing optimism upon downside surprises in April’s NFP and June’s CPI; then hard-landing fears surrounding August’s shock NFP; and, finally, ‘no-landing’ concerns in anticipation of a reflationary Trump regime.  

![Alt_text](figures/figure1.jpg)

### Regression analysis

Figure 2 shows a clear steepening of the 2s10s, relative to fair value, over the shaded sample (the average residual over this period is ~5 times the model standard error). Indeed over that sample the curve outperforms its beta to the 1y1y swap rate (Figure 3).



![Alt_text](figures/figure2.jpg)<br><br>
![Alt_text](figures/figure3.jpg)

Increases in the 1y1y rate are associated with steepening over the shaded sample, but flattening over the full sample. The change in this beta can be decomposed into changes in the betas of the 2yr and 10yr yields to the 1y1y rate across the full and restricted samples (Figure 4).

![Alt_text](figures/figure4.jpg)

Increases in the 1y1y rate cause bear flattening over the full sample (left blue bar > right blue bar) but bear steepening (left yellow < right yellow) over the shaded sample. <br><br>


# Section 2: Buying belly vol in a 2s5s10s butterfly swaption straddle as a way to position for policy uncertainty  

In this note we consider positioning for policy uncertainty by buying belly vol in a 2s5s10s butterfly swaption straddle—that is, buying two ATM straddles on the 5yr swap rate, and selling an ATM straddle on each of the 2yr and 10yr rates.  The sample period runs from 2018-07-12 to 2024-11-27.

### Straddle swaption on a 2s5s10s swap butterfly

In in fact the 5yr yield captures the full spectrum of rate expectations (short, medium and long-run), then environments characterized by high degrees of policy uncertainty should see outperformance in belly realised-vol (figure 5; figure 6). This recommends buying the belly in a 2s5s10s swaption straddle butterfly (that is, buying two ATM straddles on the 5yr swap rate, and selling an ATM straddle on each of the wing rates).

![Alt_text](figures/figure5.jpg)

![Alt text](figures/figure6.jpg) 

# Conclusion 

The 2s10s UST curve currently appears cheap relative to fair value. Much of this cheapness appears driven by a heightened beta to the 1y1y OIS rate. It could also be driven by rising term-premia, itself driven by heightened policy uncertainty, in which case buying belly vol in 2s5s10s swaption straddle butterfly would be an advisable trade. 
