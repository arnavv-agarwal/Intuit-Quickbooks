## Overview
QuickBooks is an accounting software package developed and marketed by Intuit. This analysis focuses on modeling the response to an upselling campaign for upgrading to the latest version of QuickBooks software. By employing testing and predictive analysis, the aim is to target the "right" customers for the campaign.

## Objective
The purpose of this exercise is to gain experience in modeling the response to an upsell campaign. Utilizing data on 75,000 small businesses, the goal is to predict which businesses are most likely to respond to a wave-2 mailing after not responding to the initial wave-1 mailing.

## Data
The intuit75k.rds file contains data on 75,000 businesses selected randomly from 801,821 that were sent the wave-1 mailing. The key variable 'res1' denotes which businesses responded to the mailing by purchasing QuickBooks version 3.0.

## Analysis
After running analysis on the data, three scenarios are considered:

1. Without RFM analysis: QuickBooks would mail all 22,500 customers with a predicted response rate of 4.9%.
2. With IQ targeting: QuickBooks would mail 17,983 customers with a predicted response rate of 5.67%.
3. With SQ targeting: QuickBooks would mail 18,188 customers with a predicted response rate of 5.62%.

## Logistic Regression
Logistic regression is employed for predictive analytics and modeling. It allows us to understand the relationship between the dependent variable ('res1_yes') and independent variables, predicting the likelihood of a business upgrading to the latest QuickBooks version.

### Standardize Values
Values are standardized to better scale the impact of variables.

### Odd-Ratio Interpretation
Important variables include 'version1' (2.132) and 'upgraded' (2.665), indicating a significant impact on the likelihood of a positive response.

Less important variables include 'zip_bins' (0.946) and 'dollars' (1.083), indicating less influence on the response likelihood.

Variables 'numords' (1.389) and 'last' (0.637) have medium importance, influencing the response likelihood moderately.

## Conclusion
Through this analysis, it's evident that targeted mailing based on predictive modeling can significantly improve response rates and expected profits. Logistic regression offers insights into the key variables influencing customer response, guiding targeted marketing strategies.

