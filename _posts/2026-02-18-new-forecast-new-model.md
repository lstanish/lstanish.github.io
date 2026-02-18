---
title: "New data, new evaluation, new model, new forecast!"
author: "Ryan McClure, PhD"
subtitle: All models are worng, but some are useful. -George Box
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


### Our third forecast comes with some updates

I have gone out and downloaded the latest HOBO temperature data from Grange Creek. 

![]({{ '/assets/img/1771430400_Observed_temps.png' | relative_url }})

The water temperatures seemed to remain steady. 

However, how did our forecasts starting on February 10th do?

![]({{ '/assets/img/2026-02-10_Forecast_observe_compare.png' | relative_url }})

Well, not great again. The RMSE improved slightly, but our NSE continues to get worse. This means it might be time to start exploring a new model or model covariates for our BDLM. 

With that in mind. Another covariate we can add to the model is cloud cover instead of temperature. Lets make a new forecast with incoming solar radiation and cloud cover instead of solar radiation and temperature. 

![]({{ '/assets/img/ezgif.com-animated-gif-maker.gif' | relative_url }})

OK - we have a forecast now that goes out until Feb. 24th. Let's sit tight and see how well our new prediction model performs. 

