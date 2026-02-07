---
title: "Forecasting example"
author: "Ryan McClure, PhD"
subtitle: Forecasts of water temperature in my backyard creek
gh-repo: ryanmclake/grangeCreekTempForecasts
gh-badge:
- star
- fork
- follow
tags: test
comments: true
mathjax: true
layout: post
---

This is a demo on how to forecast the most important aspect of water... temperature. This blog is an exercise that generates 7-day ahead water temperature forecasts for Grange Creek in Thornton, CO. Grange Creek is a very small, heavily urbanized, waterway that sits just behind my home. 
I strongly encourage you to [review all of the code in Github](https://github.com/ryanmclake/grangeCreekTempForecasts).

### Let's start with some simple water facts

We know some simple rules about water, and I mean let's start really simple.
+ Water has a high specific heat capacity. It absorbs a lot of heat as energy before it begins to get hot
+ When water does get hot, it can remain hot for a while before cooling down
+ My home in Denver, CO USA has seasons (summer, fall, winter, and spring). In winter, the water temperature is colder because the air temperature is cold and we get less sun. 
+ In summer, the water temperature is warmer because it is warmer outside because the air temperature is warmer and we get more sunlight. 

We can generate forecasts with information from these four simple rules. 

### Now we need some data

I went ahead and setup a HOBO data logger that I had from my PhD and secured it in my creek. The logger was set to record temperature at 15-minute intervals in GMT. It was deployed in the afternoon of January 21st. I let the sensor collect temperature data for 10 days before my first data download on Feburary 1st, 2026. 

Here is a time series (aggregated to the hour) of the water temperature in Grange Creek.
![]({{ '/assets/img/1769979600_Observed_temps.png' | relative_url }})

From this figure, we can see that there is a strong daily cycle in water temperature. Water temperature starts to warm up when the sun is out, reaching a high temperature in the evening after the sun has gone down (there is that high specific heat). The temperature then cools down from midnight into the next morning and then is really cold in the AM the next day.

What else has a cycle like this? Well, the temperature of the air and the amount of sunlight that is coming in and hitting the stream (incoming solar radiation). 

As such, let's try to generate some forecasts of Grange Creek's water temperature based on the air temperature and the amount of incoming sunlight. Deriving a prediction from another variable(s) through an equation is what we call a model. A model is a representation of reality. The model that we are using in this exercise is called a Bayesian Dynamic Linear Model (BDLM). A BDLM is useful particularly for short-term forecasting. We will use the DLM to obtain a new distribution of our model's parameters given all the information we have available up to out current state (i.e., now). 

So, what information do we have? WE have an estimated distribution of what the water temperature is, we have actual observations of the temperature of the water, we have temperature of the air and incoming solar radiation from observed met data. 

Thus, we can use our prior understanding of a system plus some data to inform a new understanding of the system with a model.

### Let's fit our model to the data. 

![]({{ '/assets/img/2026-02-01_DLM_output.png' | relative_url }})

We can see that our BDLM fits along with the observed temps well. The light blue shade is the 95% credible interval of the BDLM's prediction. The red points are the hourly aggregated water temperature observations. We also see that the model ends but there are still a few observations. I have purposefully done this so we can compare how our forecast does against actual observed data. 

What we are interested in, however, is the distribution of our parameters for our model given all of the information we have. 

Here are all of the distributions of the parameter outputs from our BDLM:
![]({{ '/assets/img/Posterior_1.png' | relative_url }})
![]({{ '/assets/img/Posterior_2.png' | relative_url }})

Ok - there is a lot to digest in the figure. To keep it simple, the left columns, are the results of a Markov-Chain Monte-Carlo that randomly samples from a distribution of our prior state to inform our new state. You can see that there are parameters associated with some common variables we've discussed (e.g., sun (betasun) and temperature (betatemp)). The other parameters are aspects of the BDLM that will go into our forecast. 

Now that we have our posterior distributions from a calibrated model, let's transition to actual out of sample forecasts. In order to get a forecast of future water temperatures in Grange Creek, we need to have actual forecast data of air temperature and incoming solar radiation. Where do we get that? 

I like to use the [Open Meteo API](https://open-meteo.com/). It is a website where you can basically download all available weather forecasts from all operational forecast models that are public.

To iteratively get the forecasts, I have leveraged the site's feature that outputs Python scripts one can use to download the forecasts and save them onto your local computer. 

So, our BDLM last time stamp was at 2026-02-01 00:00:00 (GMT). Thus, I downloaded weather forecasts of air temperature 2 meters above the ground and incoming solar radiation for the 0.25° grid that the Grange Creek water temperature is being measured that also started at 2026-02-01 00:00:00 (GMT).

Here are those forecasts. The go 7 days at an hourly time step into the future. 

Air temperature forecast (31 ensembles)
![]({{ '/assets/img/2026-02-01_MET_forecasts_TEMP.png' | relative_url }})

Solar radiation forecast (31 ensembles)
![]({{ '/assets/img/2026-02-01_MET_forecasts_SUN.png' | relative_url }})

### When the posterior distributions meet the forecast data

We now have posterior distributions of our parameters and 31 ensembles of temperature and solar radiation. We can randomly draw from our distributions 50 times and then apply all 50 random draws to an ensemble. We can then have separate random draws for all 31 ensembles, generating a total of 1550 potential futures of water temperatures in Grange Creek. 
![]({{ '/assets/img/2026-02-01_forecasts_tempSunModel.png' | relative_url }})

And there you have it. We have generated a forecast of water temperature, hourly, 7-days into the future in Grange Creek using solar radiation and air temperature. 

However, at first glance we can see that the forecast is underestimating the water temperatures that we see in the next day. As such, developing a new forecast in another 10 days or so with new information may yield a better forecast. 
