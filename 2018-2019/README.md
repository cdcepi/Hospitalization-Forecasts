This folders contains hospital forecasts submitted during the 2018-2019 influenza season. Each folder contains submissions from a single forecasting model. Further details about the forecasts are available below. 

# Background
When and where flu increases will occur, how large the impact of the flu season will be, and when the flu season will peak varies from season to season, making the preparation for and response to the influenza seasons difficult. Flu forecasting can change that by offering the possibility to look into the future and better plan ahead, potentially reducing the impact of flu.

To help support the development of the science of flu forecasting and its application for public health, CDC, through the Epidemic Prediction Initiative (EPI), has organized FluSight challenges to forecast the timing, intensity, and short-term activity of the influenza season since the 2013-14 season. These challenges have provided the scientific and public health community experience in real-time forecasting, the ability to evaluate forecast accuracy, and experience in communicating and applying these forecasts in real-world settings. For example, forecasts are currently used to inform CDC’s activity summaries provided to public health officials and CDC leadership and public messaging regarding the timing of the influenza season and how the public can protect themselves and their family.

As part of the forecasting initiative, CDC has developed, through EPI, the “FluSight” flu forecasting website, which facilitates the real-time sharing and visualization of weekly flu forecasts. Visitors to this site can view current and past forecasts throughout the flu season for the start and peak week, peak intensity, and the near-term activity at the national and regional levels. ILINet data are generally updated every Friday, and forecasts are generally available by Tuesday. During the 2019–20 season, CDC expects forecasting teams to provide over 30 national-level forecasts each week.

# Forecast Targets
For each week during the season, participants will be asked to provide overall and age-group specific probabilistic forecasts for the entire influenza season (seasonal targets) and for the next four weeks (four-week ahead targets). The seasonal targets are the peak week and the peak weekly hospitalization rate of the 2018-19 influenza season. The four-week ahead targets are the weekly rate of influenza hospitalizations one week, two weeks, three weeks, and four weeks ahead from date of the forecast.

## Seasonal Peak Week
**Definition:** The peak week will be defined as the MMWR surveillance week that the weekly FluSurv-NET hospitalization rate, rounded to one decimal place, is the highest for the 2018-19 influenza season.

**Motivation:** Accurate and timely forecasts for the peak week can be useful for planning and promoting activities to increase influenza vaccination prior to the bulk of influenza illness. For healthcare, pharmacy, and public health authorities, a forecast for the peak week can guide efficient staff and resource allocation.

## Seasonal Peak Rate
**Definition:** The intensity will be defined as the highest numeric value, rounded to one decimal place, that the weekly FluSurv-NET hospitalization rate reaches during the 2018-19 influenza season.

**Motivation:** Accurate and timely forecasts for the peak week and intensity of the influenza season can be useful for influenza prevention and control, including the planning and promotion of activities to increase influenza vaccination prior to the bulk of influenza illness. For healthcare, pharmacy, and public health authorities, a forecast for the peak week and intensity can help with appropriate staff and resource allocation since a surge of patients with influenza illness can be expected to seek care and receive treatment in the weeks surrounding the peak.

## Short Term Forecasts
**Definition:** One- to four-week ahead forecasts will be defined as the weekly FluSurv-NET hospitalization rate, rounded to one decimal place.

**Motivation:** Forecasts capable of providing reliable estimates of influenza hospitalizations over the next month are critical because they allow healthcare and public health officials to prepare for and respond to near-term changes in influenza activity and bridge the gap between reported incidence data and long-term seasonal forecasts.

# FluSurv-NET Data
Data on the weekly rate of influenza hospitalizations is reported through the FluSurv-NET system for the United States as a whole, as well as for individual FluSurv-NET sites. Rates are reported for specific age groups as well as an overall rate. These data can be accessed directly from [CDC](https://gis.cdc.gov/GRASP/Fluview/FluHospRates.html) or the R package cdcfluview. 

# Forecast Evaluation
All forecasts will be evaluated using the weighted observations pulled from the FluSurv-NET system in week 28, and the logarithmic score will be used to measure the accuracy of the probability distribution of a forecast. Logarithmic scores will be averaged across different time periods, the seasonal targets, the four-week ahead targets, and locations to provide both specific and generalized measures of model accuracy. Forecast accuracy will be measured by log score only. Nonetheless, forecasters are requested to continue to submit point predictions, which should aim to minimize the absolute error (AE).

## Logarithmic Score
If p is the set of probabilities for a given forecast, and pi is the probability assigned to the observed outcome i, the logarithmic score is:

S(p,i)=ln(pi)

For peak week, the probability assigned to that correct bin (based on the observed FluSurv-NET) plus the probability assigned to the preceding and proceeding bins will be summed to determine the probability assigned to the observed outcome. In the case of multiple peak weeks, the probability assigned to the bins containing the peak weeks and the preceding and proceeding bins will be summed. For peak weekly rate and 1-4 week-ahead forecasts, the probability assigned to the correct 0.1 bin plus the probability assigned to the age group-specific number of preceding and following bins will be summed to determine the probability assigned to the observed outcome, with a minimum of 1 preceding and following bin. For each age group, and for overall rates, bins including up to plus or minus 10% of the observed value will be applied to each side of the observed value, rounded to the nearest 0.1. For example, if the observed overall peak hospitalization rate is 3.3 per 100,000, the bins encompassing 10% of this value (0.3) above and below the observed value of 3.3 will be included. Therefore, the probabilities assigned to all bins ranging from 3.0 to 3.6 would be summed to determine the probability assigned to the observed outcome.

In the case of very small observed values, a minimum of one bin proceeding and following the observed bin will be included with the observed bin. For example, if the observed weekly hospitalization rate is 0.2 per 100,000, the probabilities assigned to bins representing 0.1 and 0.3 will also be included. For all targets, if the correct bin is near the first or last bin, the number of bins will be truncated at the respective boundary. Undefined natural logs (which occur when the probability assigned to the observed outcome was 0) will be assigned a value of -10. Forecasts which are not submitted (e.g. if a week is missed) or that are incomplete (e.g. sum of probabilities greater than 1.1) will also be assigned a value of -10.

Example: At the conclusion of the season, FluSurv-NET showed that the 2016/2017 overall weekly hospitalization rates peaked at 5.4 per 100,000. As a result, the window of plus or minus 0.54 rounds to 0.5, which spans the probability bins from 4.9 to 5.9. If a forecast predicts there is a probability of 0.1 (i.e. a 10% chance) that hospitalization rates peak at 5.4 per 100,000, with an additional 0.3 probability that they peak between 4.9 and 5.3 and a 0.2 probability that they peak between 5.5 and 5.9, then the forecast would receive a score of ln(0.6)=−0.51. If the season peaked on another week, the score would be calculated on the probability assigned to that week plus the values assigned to the preceding and proceeding week.

# R Package
FluSight Package
The FluSight R package contains functions to help create and format forecasts, read and verify forecast CSVs, and score forecasts. These are the functions that will be used at CDC to verify and score submitted forecasts. Teams are welcome to use these tools to ensure their forecasts fit the required template and score their forecasts prior to receiving official scores from CDC

The package can be downloaded from [GitHub](https://github.com/jarad/FluSight).

Install and load package
```
devtools::install_github("jarad/FluSight")
library(FluSight)
```
Read in entry CSV
```
entry <- read_entry("your_csv.csv")
```
Verify entry
```
verify_entry(entry)
verify_entry_file("your_csv.csv")
```
Create file of observed truth from CDC surveillance data
```
truth <- create_truth(fluview = T, year = 2018)
```
Expand observed truth to take into account additional bins - 1 bin for weeks, 5 bins for percentage
```
exp_truth <- expand_truth(truth, week_expand = 1, percent_expand = 5)
```
Score a weekly entry against the observed truth
```
exact_scores <- score_entry(entry, truth)
expand_scores <- score_entry(entry, exp_truth)
```
# References
Gneiting T and AE Raftery. (2007) Strictly proper scoring rules, prediction, and estimation. Journal of the American Statistical Association. 102(477):359-378. Available at: https://www.stat.washington.edu/raftery/Research/PDF/Gneiting2007jasa.pdf

Rosenfeld R, J Grefenstette, and D Burke. (2012) A Proposal for Standardized Evaluation of Epidemiological Models. Available at: http://delphi.midas.cs.cmu.edu/files/StandardizedEvaluationRevised12-11-09.pdf.
