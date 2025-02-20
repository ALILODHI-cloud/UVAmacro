[View the code that generated this analysis (Python Juypter Notebooks)](https://github.com/ALILODHI-cloud/UVAmacro.github.io/blob/main/post_1/analysis.ipynb)

# Buying belly vol in a 2s5s10s butterfly swaption straddle as a way to position for policy uncertainty

The 2-year treasury yield reflects near-term Fed pricing, whereas the 10-year treasury yield reflects both longer-term Fed pricing, and the premium commanded by duration risk. If indeed belly-rates - the 5-year rate, for instance - captures both these considerations, then periods of heightened policy should see realised volatility on the 5-year rate outperform that on the 2-year and 10-year ones (Figure 5; Figure 6). The intuition is that the 5-year rate is giving expression to two sources of uncertainty, whereas each of the 2-year and 10-year are doing this only for one. But why, per Figure 6, is this not a general phenomenon, obtaining also in environments characterised by 'low' and 'regular' degrees of policy uncertainty? After all, isn't the 5-year _always_ giving expression to near-term policy pricing considerations, and also to long-term policy pricing\term premium considerations? A possibility is that it is only doing each of these things in times of heightened uncertainty. For instance, near-term policy pricing uncertainty only ripples up into the belly when there is a lot of it - because considerable near-term pricing uncertainty typically entails considerable medium-term pricing uncertainty. The same can be argued for long-term policy pricing rippling down into the belly. As for long-term tp uncertainty: its reasonable to think that it induces uncertainty around tp for belly duration only where is a considerable amount of it (a considerable amount of long-term tp uncertainty, that is).

One way to position for this kind of belly vol outperformance is via the 2s5s10s butterfly swaption straddle. 


*remove annualised from graph*

![Alt_text](figures/figure5.jpg)

![Alt text](figures/figure6.jpg) 

One way to position for this kind of belly vol outperformance is via the 2s5s10s butterfly swaption straddle. 


## 2s5s10s butterfly swaption straddle

This trade is executed by buying an ATM straddle on the 5-year rate, and selling an ATM straddle on each of the 2-year and 10-year rates. Below we provide a brief primer on swaptions and straddles. 

### Primer: the mechanics swaptions and straddles

By buying a 'payer swaption', I buy the right to enter an interest rate swap as the payer of a given fixed rate (the 'strike rate'), and a receiver of a particular floating rate (typically the OIS rate). If the swaption is 'AT-THE-MONEY' ('ATM'), then the strike rate is equal to the prevailing fixed rate for swaps of that tenor. So, for instance, if I buy an ATM swaption on a 2-year swap, strike rate will equal to the prevailing fixed-rate on a 2-year swap. In turn, this fixed-rate has been priced such that it equals the expected average of the OIS rate over the next two years, and thus so too has the strike rate in my swaption. Because of this, in expectation I would earn a payoff of zero were I to enter the swap immediately ('exercise' the swaption). But consider that the 2-year swap rate rises above the strike rate (because of, say, a hawkish repricing of the Fed). This means that the expected average of the OIS rate, over the next two years, is greater than the strike rate. Now, my expected from exercising the swaption is greater than zero, and so it is profitable for me to do so. But what is also the case is that the swaption, as a position, has gained in value. So in principle I could sell it for a profit. Two other details warrant mentioning. First, for reasons made clearly previously, its value is increasing in the underlying 2-year swap rate. Second, the sensitvity of its value to small increases in the underlying 2-year swap rate (or 'delta'), is itself positively correlated with the underlying swap rate. So a +1 increase in the 2-year rate when the 2-year rate = the strike rate will induce, say, a 4-unit appreciation in the value of the position, but then a subsequent +1 increase will induce a 7-unit appreciation, etc. On the other hand a fall in the 2-year swap rate will mean that subsequent falls cause progressively less depreciation in the value of the position. All this is reversed for a receiver swaption (so increases in teh 2-year swap rate will mean depreciation in the value of the position, but by a progressively diminishing magnitude; and decreases in that rate will mean appreciation in the value of the position, and at a progressively increasing magnitude).  

A swaption straddle buddles a receiver swaption and a payer swaption. Both swaptions begin ATM. Also, both begin with the same delta. So if the 2-year swap rate nudges up marginally, then the appreciation of the payer will be exactly offset by the depreciation of the receiver. But per our previous discussion, further increases in the 2-year rate will see appreciation of the payer that exceeds the depreciation on the receiver, and thus a net gain.  


A straddle, recall, comprises one ATM payer swaption, and one ATM receiver swaption. The position is initiated such that both swaptions have the same delta (4, say). This means that, if the underlying rate move incrementally upwards, then the payer swaption will gain 4, and the receiver swaption will lose 4 - so-called 'delta-neutrality', or a neutrality of the value of the straddle to small movements in the underlying rate. But because the underlying rate has changed, so will have the deltas of each swaption. Because the delta of a payer swaption increases with the underlying rate, the delta of that position is now 6, say. Conversley, because the delta of a receiver swaption _decreases_ with the underlying rate, the delta of that position is now 2, say. Upon further increases in the underlying rate, gains on the payer > losses on the receiver, and the straddle gains in value. But suppose the underlying rate had increased wildly at the get-go - something like 40bp. Overall, the gain on the payer, from this move, will far outweigh the losses on the receiver - and vice versa if the underlying had _decreased_ by 40bp. So, one instance when a straddle outperforms is upon realisation of large movement in the underlying rate, in whichever direction. Thus, a straddle is a way position for such swings, in the event that they are anticipated. 



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
