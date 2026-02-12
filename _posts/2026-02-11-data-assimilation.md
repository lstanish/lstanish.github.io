---
title: "Data Assimilation"
author: "Ryan McClure, PhD"
subtitle: Does not have to be as complicated as you think
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


### Let's do some bulk data assimilation

It is important to note that data assimilation (DA) is an entire discipline that folks litterally dedicate their entire careers to. Simply put, DA is a tool to update a model with new information before making a new prediction. The best example of this that folks hear about is a Kalman Filter. This was the method used to steer the Saturn V rockets for the moon missions. 

We are not implementing a Kalman filter in this simple exercise. Check back soon for that post. Here, we are going to do a simple method called bulk data assimilation. In other words, when new data are available we rerun the entire Bayes Dynamic Linear Model (BDLM) with the new data, then use the newest posteriors to generate our forecast. This appraoch is more computationally intensive than other methods, but it is a great way to show how much the coefficients in our models shift through time and increase or decrease in variance. 

Our BDLM has four key coefficients that go into making our predictions, the coefficient for the incoming solar radiation, for the temperature, for our autoregressive temperaute (temperature the prior hour), and our intercept. When we generated our first forecast on Feb 1st, each of these coefficients had a distribution of possible values based on our BDLM calibration. We randomly drew from these distributions and made the forecast. 

However, we also know that our forecast did not do that great when we compared the mean of the forecasts against the observations. As such, this might imply that our coefficients were not that helpful. What we will see now is how the coefficient distributions change daily with new incoming data from our most recent HOBO download. 

The four images below are stacked density plots of each of the coefficients in our model. The date of our first forecast (Feb 1st) is on the bottom. Then I have rerun the BDLM model with new temperature for Feb 2nd, 3rd, 4th, ... all the way up to Feb 10th, which are the latest posterior distributions that we will use for our new forecast that will occur on Feb 10th. 

Here is the daily density plots of the coefficient for temperature
![]({{ '/assets/img/DA_Betatemp_output.png' | relative_url }})

for incoming solar radiation
![]({{ '/assets/img/DA_Betasun_output.png' | relative_url }})

for the prior temperature
![]({{ '/assets/img/DA_BetaX_output.png' | relative_url }})

and for the intercept
![]({{ '/assets/img/DA_INT_output.png' | relative_url }})

What are some of the patterns you see?

Let's start with the temperature coefficient. The mean does not seem to change much but it is quite apparent that each sequential density plot increases in variance, meaning we are less and less confident in temperature as a predictor as we get more data. Interesting! 




