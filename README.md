## Overview
<p align="justify">QuickBooks is an accounting software package developed and marketed by Intuit. This analysis focuses on modeling the response to an upselling campaign for upgrading to the latest version of QuickBooks software. By employing testing and predictive analysis, the aim is to target the "right" customers for the campaign.</p>

## Objective
<p align="justify">The purpose of this exercise is to gain experience in modeling the response to an upsell campaign. Utilizing data on 75,000 small businesses, the goal is to predict which businesses are most likely to respond to a wave-2 mailing after not responding to the initial wave-1 mailing.</p>

## Data
<p align="justify">The intuit75k.rds file contains data on 75,000 businesses selected randomly from 801,821 that were sent the wave-1 mailing. The key variable 'res1' denotes which businesses responded to the mailing by purchasing QuickBooks version 3.0.</p>

## Recency, Frequency & Monetary Charts (RFM)

- Recency Chart
  - <p align="justify">The below graph depicts the proportion of customers who responded "yes" to waive 1 mail that was send out, per independent recency. The customers in bin 1 had the     highest response rate from the mail sent out as opposed to ones in bin 5. It shows that the response rate from the top quintile (20% group) was 9.00%, while the next quintile responded at a rate of ~5.4%. The last quintile had a response rate of ~2.3%.</p>

```python 
fig1 = rsm.prop_plot(intuit75k[intuit75k['training']==1], "rec_iq", "res1", "Yes")
fig1 = fig1.set_xlabel("Recency value quintiles (rec_iq)")
```
<p align="center">
  <img width="460" height="300" src="https://github.com/arnavv-agarwal/Intuit-Quickbooks/blob/main/R.png">
</p>

- Frequency Chart
  - <p align="justify">The below graph depicts the proportion of customers who responded "yes" to waive 1 mail that was send out, per independent frequency. The customers in bin 1 had the highest frequency rate from the mail sent out as opposed to ones in bin 5. The customers in bin 1 had the highest response rate from the mail sent out as opposed to ones in bin 5. It shows that the response rate from the top quintile (20% group) was 8.00%, while the next quintile responded at a rate of 5.00%. The last quintile had a response rate of ~3.3%.</p>
  
```python 
fig2 = rsm.prop_plot(intuit75k[intuit75k['training']==1], "freq_iq", "res1", "Yes")
fig2 = fig2.set_xlabel("Frequency value quintiles (freq_iq)")
```
<p align="center">
  <img width="460" height="300" src="https://github.com/arnavv-agarwal/Intuit-Quickbooks/blob/main/F.png">
</p>

- Monetary Chart
  - <p align="justify">The above graph depicts the proportion of customers who responded "yes" to waive 1 mail that was send out, per independent monetory. The customers in bin 1 had the highest expenditure rate from the mail sent out as opposed to ones in bin 5. It shows that the response rate from the top quintile (20% group) was 7.00%, while the next quintile responded at a rate of 4.5%. The last quintile had a response rate of 3.2%.</p>

```python 
fig3 = rsm.prop_plot(intuit75k[intuit75k['training']==1], "mon_iq", "res1", "Yes")
fig3 = fig3.set_xlabel("Monetary value quintiles (mon_iq)")
```
<p align="center">
  <img width="460" height="300" src="https://github.com/arnavv-agarwal/Intuit-Quickbooks/blob/main/M.png">
</p>

## RFM Index
To perform RFM analysis, we bin the customers using Independent or Sequential Method. In independent method, the ranks of RFM are assigned independently.

- Independent 
```python 
intuit75k = intuit75k.assign(
    rfm_iq=intuit75k.rec_iq.astype(str)
    + intuit75k.freq_iq.astype(str)
    + intuit75k.mon_iq.astype(str)
)
```
```python 
plt.figure(figsize=(16, 7))
# fig = rsm.prop_plot(bbb, "rfm_iq", "buyer", "yes", breakeven=breakeven)
fig = rsm.prop_plot(intuit75k, "rfm_iq", "res1", "Yes")
fig.set_xticklabels(fig.get_xticklabels(), rotation=90)
fig = fig.set(xlabel="Independent RFM index (rfm_iq)")
```
<p align="center">
  <img width="600" height="300" src="https://github.com/arnavv-agarwal/Intuit-Quickbooks/blob/main/RFMI.png">
</p>

- Sequential
  - <p align="justify">To further modify the RFM analysis, we use sequential method to assign the ranks of RFM in order. In this method, first the Recency values are assigned. Then within each recency rank, customers are assigned a frequency rank, and within each frequency rank, customer are then assigned a monetary rank. This tends to take into account all the three factors in each bin value and hence provide a better even distribution of combined RFM scores.</p>
  
```python 
intuit75k = intuit75k.assign(
    rfm_sq=intuit75k.rec_iq.astype(str)
    + intuit75k.freq_sq.astype(str)
    + intuit75k.mon_sq.astype(str)
)

intuit75k.head()
```
```python 
plt.figure(figsize=(16, 7))
# fig = rsm.prop_plot(bbb, "rfm_iq", "buyer", "yes", breakeven=breakeven)
fig_rfm_sq = rsm.prop_plot(intuit75k, "rfm_sq", "res1", "Yes", breakeven = breakeven)
fig_rfm_sq.set_xticklabels(fig_rfm_sq.get_xticklabels(), rotation=90)
fig_rfm_sq = fig_rfm_sq.set(xlabel="Independent RFM index (rsm_sq)")
```
<p align="center">
  <img width="600" height="300" src="https://github.com/arnavv-agarwal/Intuit-Quickbooks/blob/main/RFMS.png">
</p>

## Analysis
After running analysis on the data, three scenarios are considered:

1. Without RFM analysis: QuickBooks would mail all 22,500 customers with a predicted response rate of 4.9%.
2. With IQ targeting: QuickBooks would mail 17,983 customers with a predicted response rate of 5.67%.
3. With SQ targeting: QuickBooks would mail 18,188 customers with a predicted response rate of 5.62%.

## Why try models apart from RFM?
<p align="justify">The result of modeling using RFM is that Intuit will mail to their most responsive customers, and will neglect all of the others. That means that they will get absolutely no attention, and will eventually end up losing them. This is OK for few customers, who are worthless anyway. But Intuit would want to try to hang on to the rest of their customers who, with a little attention can be persuaded to move up to a more profitable RFM cell. Our marketing should be designed to encourage customers in some cells to do just that.</p>

## Logistic Regression
<p align="justify"> Logistic regression is employed for predictive analytics and modeling. It allows us to understand the relationship between the dependent variable ('res1_yes') and independent variables, predicting the likelihood of a business upgrading to the latest QuickBooks version.</p>

```python 
lr_std_df2 = smf.glm(
    formula="res1_yes ~ zip_bins + numords + dollars + last + version1 + upgraded",
    family=Binomial(link=logit()),
    data=intuit75k_std_df1,
).fit()
print(rsm.or_ci(lr_std_df2))
```
### Standardize Values
Values are standardized to better scale the impact of variables.

### Odd-Ratio Interpretation
- Important variables include 'version1' (2.132) and 'upgraded' (2.665), indicating a significant impact on the likelihood of a positive response.
- Less important variables include 'zip_bins' (0.946) and 'dollars' (1.083), indicating less influence on the response likelihood.
- Variables 'numords' (1.389) and 'last' (0.637) have medium importance, influencing the response likelihood moderately.

## Conclusion
<p align="justify"> Targetting Quickbooks with logit would email all 27,579 (122.57%) customers. The response rate for the selected customers is predicted to be 8.58% or 2,367 buyers. The revenue is equal to $142,020. The expected profit is $35,059. The email cost is estimated to be $38,886 with a ROME of 265.22%.</p>


