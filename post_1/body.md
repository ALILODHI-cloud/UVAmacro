[View the code that generated this analysis (Python Juypter Notebooks)](https://github.com/ALILODHI-cloud/UVAmacro.github.io/blob/main/post_1/analysis.ipynb)


# Buying belly vol in a 2s5s10s butterfly swaption straddle as a way to position for policy uncertainty


>**Summary**
>
> Historically, the 2s5s10s butterfly swaption straddle (buying two straddles on the 5 vs selling a straddle on each of the 2 and 10) outperforms during periods of heightened policy uncertainty, relative to periods with less such uncertainty. The realised volatility of the Fed Funds curve is used as a proxy for policy uncertainty. 




\
The 2-year treasury yield reflects near-term Fed pricing, whereas the 10-year yield reflects both longer-term Fed pricing, and the premium commanded by duration risk. If indeed belly-rates - the 5-year rate, for instance - capture both these considerations, then periods of heightened policy uncertainty should see realised volatility on the 5-year rate outperform that on the 2-year and 10-year ones (Figure 1; Figure 2). The intuition is that the 5-year rate is giving expression to two sources of uncertainty, whereas each of the 2-year and 10-year are doing this only for one. But why, per Figure 2, is this not a general phenomenon, obtaining also in environments characterised by 'low' and 'regular' degrees of policy uncertainty? After all, isn't the 5-year _always_ giving expression to near-term policy pricing considerations, and also to long-term policy pricing/term premium considerations? A possibility is that it is only doing each of these things in times of heightened uncertainty. For instance, near-term policy pricing uncertainty only ripples up into medium-term policy pricing uncertainty when there is a lot of it. The same can be argued for long-term policy pricing rippling down into the belly. As for long-term tp uncertainty: it's reasonable to think that it induces uncertainty around belly duration tp only when there is a considerable amount of it. 

![Alt_text](figures/figure1.jpg)

![Alt text](figures/figure2.jpg) 


One way to position for this kind of belly vol outperformance is via the 2s5s10s butterfly swaption straddle. 


## 2s5s10s butterfly swaption straddle

This trade is executed by buying two ATM straddles on the 5-year rate, and selling an ATM straddle on each of the 2-year and 10-year rates. Below we provide a brief primer on swaptions and straddles. 


> ### Primer: swaptions and swaption straddles
>
>By buying a 'payer swaption', I buy the right to enter an interest rate swap as the payer of a given fixed rate (the 'strike rate'), and a receiver of a particular floating rate (typically the OIS rate). If the swaption is 'AT-THE-MONEY' ('ATM'), then the strike rate is equal to the prevailing fixed rate for swaps of that tenor. For instance if I buy an ATM swaption on a 2-year swap, the strike rate will equal to the prevailing fixed-rate on a 2-year swap. In turn, this fixed-rate has been priced such that it equals the expected average of the OIS rate over the next two years, and thus so too does the strike rate in my swaption. Because of this, in expectation I would earn a payoff of zero were I to enter the swap immediately (in particular, the present value of the flow of payments I will make = present value of flow of payments I will receive). But suppose that the 2-year swap rate rises above the strike rate (because of, say, a hawkish Fed repricing). This means that the expected average of the OIS rate, over the next two years, is greater than the strike rate. Now, my expected payoff from exercising the swaption is greater than zero, and so it is profitable for me to do so. But what is also the case is that the swaption, as a position, has gained in value. So in principle I could sell it for a profit. 
>
>Two other details warrant mentioning. First, for reasons made clear previously, a payer swaption's value is increasing in the underlying 2-year swap rate. Second, the rate at which this is occuring is itself increasing in the underlying swap rate. So a +1 increase in the 2-year rate when the 2-year rate = the strike rate will induce, say, a 4-unit appreciation in the value of the position, but then a subsequent +1 increase will induce a 7-unit appreciation, etc. On the other hand, a fall in the 2-year swap rate will mean that subsequent falls cause progressively less depreciation in the value of the position. All this is reversed for a receiver swaption (so increases in the 2-year swap rate will mean depreciation in the value of the position, but by a progressively diminishing magnitude; and decreases in that rate will mean appreciation in the value of the position, and by a progressively increasing magnitude).  
>
>A swaption straddle buddles a receiver swaption and a payer swaption. Both swaptions begin ATM. Also, both begin with the same delta. So if the 2-year swap rate nudges up marginally, then the appreciation of the payer will be exactly offset by the depreciation of the receiver. Suppose however that things begin with a 40bp jump in the 2-year rate. We can think of this as follows. The first +1 bp increase will lead to no net increase in the value of the straddle. But now the delta of the payer > delta of the receiver. So the second +1 bp will induce appreciation of the straddle. Indeed, upon each additional +1 bp rise, the straddle will appreciate, and that too by a progressively increasing magnitude (as the payer-receiver delta differential widens). The result is a large appreciation in the value of the swaption (as the gain on the payer far exceeds the loss on the receiver). 
>
>In sum: large increase (decrease) in 2-year rate --> large appreciation of payer (receiver) relative to depreciation of receiver (payer) --> large appreciation of straddle. So clearly a straddle on the x-tenor rate is long on the realised volatility of that rate.

So the best case for our butterfly trade is if the 5-year rate ends up wildly higher or lower, whereas the 2-year and 10-year end up relatively closer to their respective strikes. This is roughly equivalent to the case where 2*realised vol 5-year - (vol 2-year + vol 10-year) > 0 (its true, neither imply the other; high vol with a high degree of mean reversion entails a rate that never deviates too far from where it started,; and its possible that a rate ends up far from where it started, while proving minimally volatile over a given period - e.g. imagine a large move upwards and then flatlining for the rest of the period). In any case, should the total appreciation of the bought straddles > total appreciation of sold straddles, then we can close the position (by selling the 5-year straddle, and buying back the 2-year and 10-year ones) for a profit. Note that we want to buy back the sold straddles to eliminate the risk they might be exercised, in which case we will be forced to enter into a swap (of course this might also prove profitable but for now we abstract from that possibility).  


**Ali Lodhi**

