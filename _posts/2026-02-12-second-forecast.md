---
title: "New forecast after data assimilation"
author: "Ryan McClure, PhD"
subtitle: We can make a new forecsat since our model is updated
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
thumbnail-img: /assets/img/ecoforecastingloop.jpg
share-img: /assets/img/ecoforecastingloop.jpg
---


### Our second forecast!

We have performed a bulk data assimilation exercise in the [prior post](https://ryanmclake.github.io/mclakeconsulting.github.io/2026-02-11-data-assimilation/). Hence, we have updated our model's coefficients and initial conditions with an additional ten days of hourly water temperature data in the creek. I have appended new covariate data to match the observed temperatures, and have also downloaded a new NOAA GEFS weather forecast that starts on Feb 10th at 00:00 GMT. Putting these all together, we have a newly calibrated BDLM with new posteriors that will go into making our new water temperature forecast in Grange Creek. 

And here is that forecast.
![]({{ '/assets/img/2026-02-10_forecasts_tempSunModel.png' | relative_url }})

For viewing clarity, I have removed the prior 20+ days of the BDLM calibration and have only plotted the observations and calibrated model for the day before we hand-off to our forecast. As we can see in the figure, there is a bit more variability among all of the forecast ensembles compared to our [first forecast](https://ryanmclake.github.io/mclakeconsulting.github.io/2026-02-04-sample-forecasts/). This is because I have included a new source of uncertainty called model process error. Essentially, the source of forecast variation before came from the forecasted driver data uncertainty and the coefficient uncertainty. This new source of error integrates the error from the model (think of it like the SD of the residuals) itself into the 1550 ensembles. Stay tuned for the next post where we will tackle a hefty but important topic, uncertainty partitioning. 