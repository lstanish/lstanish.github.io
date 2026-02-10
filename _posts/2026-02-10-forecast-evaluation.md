---
title: "Forecast Evaluation"
author: "Ryan McClure, PhD"
subtitle: How did our water temperature forecasts do?
gh-repo: ryanmclake/grangeCreekTempForecasts
gh-badge:
- star
- fork
- follow
tags: test
comments: true
mathjax: true
layout: post
cover-img: /assets/img/fcr_3.jpg
thumbnail-img: /assets/img/fcr_3.jpg
share-img: /assets/img/fcr_3.jpg
---

### So, how did our forecast do?

It has been almost ten days since we have made our original forecast. As such, this allows us to take a chance to evaluate how well our forecasts performed against real observations. My daughter and I downloaded the temperature data on our way to daycare. 

These are the raw observed water temperatures in Grange Creek.
![]({{ '/assets/img/1770735600_Observed_temps.png' | relative_url }})

We can clearly see that water temperatures still maintain the diel cycle but then have a steady trend of warming day to day. I wonder if that was caputured in our forecast?

This was our original forecast on Feb. 1st
![]({{ '/assets/img/2026-02-01_forecasts_tempSunModel.png' | relative_url }})

There does not appear to be an increasing trend. However, lets quantitatively assess how well the forecast actually did instead of just visualizing it. 

To do this, a common metric to assess how well a forecast does is to calculate the Root Mean Square Error (RMSE). The advantage of RMSE is that it is in the units of the value of interest, so in our case it is in C. 
Another metric that I prefer to use over RMSE is the Nash-Sutcliffe Efficiency (NSE). NSE is normalized and lies in units from -infinity to 1. If the values is less than zero than the mean of the observations is better at predicting than the model itself. If the values are between 0 and 0.5 than the model performs better than the mean but it still needs improvement, and then values between 0.5 and 1 usually indicate that the model is performing well at predicting the variable of interest. 

I have plotted the mean of the forecast ensembles and the hourly aggregated observations and then have also quantified the RMSE and NSE. 
![]({{ '/assets/img/2026-02-01_Forecast_observe_compare.png' | relative_url }})

## So, how did our model do?

Not great. The RMSE is 3 (for temps we generally want less than 1) and NSE was -0.88 (oof!, that is not great!), but because it is a low score does not mean that is bad or wrong. That means we have gained new insights to improve our model before the next forecast. It appears that the model captures the diel cycling, but it is not capturing the highest temperatures nor the increasing trend day to day.

With this in mind, we have new data we downloaded and that means we can update our model again with this increasing trend in temperature and then make a new forecast. 

Stay tuned for a post on data assimilation and then generating a new forecast based on our latest updates to the model parameters. 


