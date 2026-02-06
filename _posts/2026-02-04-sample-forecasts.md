---
layout: post
title: Forecasting example
subtitle: Forecasts of water temperature in my backyard creek
gh-repo: ryanmclake/grangeCreekTempForecasts
gh-badge: [star, fork, follow]
tags: [test]
comments: true
mathjax: true
author: Ryan McClure, PhD
---

This is a demo on how forecast the most important aspect of water... temperature. We will go through an exercise that generates 7-day ahead water temperature forecasts for Grange Creek in Thornton, CO. It is a very small, heavily urbanized, stream that sits just behind my home. My daughter love to play in it after school. 
I strongly encourage you to [take review all of the code in Github](https://github.com/ryanmclake/grangeCreekTempForecasts).

#So how does a forecasting workflow work?

## Let's start with what we know

We know some simple rules of water physics, and I mean let's start really simple here.
+ Water has a high specific heat capacity—it absorbs a lot of heat as energy before it begins to get hot.
+ When it does get hot, it can remain hot for a while before cooling down.
+ My home in Denver, CO USA has seasons (summer, fall, winter, and spring). In winter, the water temperature is colder because the air temperature is cold and we get less sun. 
+ In summer, the water temperature is warmer because it is warmer outside because the air temperature is warmer and we get more sunlight. 

We can generate forecasts with information from these four bullets. 

##First, we need some initial data

I went ahead and used an old HOBO data logger that I have from my PhD and secured it in my creek. 

The logger was set to record temperature at 15-minute intervals in GMT. It was deployed in the afternoon of January 21st. 

I let the sensor collect temperature data for 10 days before my first data download on Feburary 1st, 2026. 

Here is a time series (aggregated to the hour) of the water temperature in Grange Creek behind the house.

![]({{ '/assets/img/1769979600_Observed_temps.png' | relative_url }})

From this figure, we can see that there is a strong daily cycle in water temperature. Water temperature starts to warm up when the sun is out, reaching a high temperature in the evening after the sun has gone down (there is that high specific heat). The temperature then cools down from midnight into the next morning and then is really cold in the AM the next day.

What else has a cycle like this? Well, the temperature of the air and the amount of sunlight that is coming in and hitting the stream (incoming solar radiation). 

Let's try to generate some forecasts of Grange Creek's water temperature based on the air temperature and the amount of incoming sunlight.

Deriving a prediction from another variable(s) through an equation is what we call a model. A model is a representation of reality. The model that we are using in this exercise is called a dynamic linear model (DLM). A DLM is useful particularly for short-term forecasting, which we are doing here. 

DLM's usually rely on Bayes theorem. To avoid the weeds of Bayes, simply put, we will use the DLM to obtain a new distribution of our model's parameters given all the information we have available up to out current state (i.e., now). 

So what information do we have? We have temperature of the water, we have temperature of the air, and we have the incoming solar radiation. 

Thus, we can use all of this information to derive a distribution of our parameter estimates of our model given the information we have. 

Let's fit our model to the data. 

![]({{ '/assets/img/2026-02-01_DLM_output.png' | relative_url }})

We can see here that our DLM fits onto the observed temps very well. The light blue shade is the 95% credible interval of the model's prediction. The red points are the hourly water temperature observations. We also see that the model ends but there are still a few observations. I have purposefully down this so we can compare how our forecast does against actual observed data. 

What we are interested in, however, is the distribution of our parameters for our model given all of the information we have. 

Here are all of the distributions of the parameter outputs from our DLM:
![]({{ '/assets/img/Posterior_1.png' | relative_url }})
![]({{ '/assets/img/Posterior_2.png' | relative_url }})

Ok - there is a lot to digest above. To keep it simple, the left columns, are the results of a Markov-chain Monte-carlo to predict the distribution of our parameters we're interested in. You can see that there are parameters associated with some common variables we've discussed (e.g., sun (betasun) and temperature (betatemp)). The other parameters are aspects of the DLM that will go into our forecast. 

Now that we have our posterior distributions from a calibrated model, let's transition to actual forecasts. In order to get a forecast of future water temperatures in Grange Creek, we need to have actual forecast data of air temperature and incoming solar radiation. Where do we get that? 

Sadly, not your phone or your weather station. Rather, we can use the same raw source that weather apps use and charge you for (which is bogus in my opinion).

I like to use the [Open Meteo API](https://open-meteo.com/). It is a website where you can basically download all available weather forecasts from all operational forecast models that are openly available. It is really cool. 

To iteratively get the forecasts, I have leveraged the site's feature that outputs Python scripts one can use to download the forecasts and save them onto your local computer. 

So, our DLM ended exactly at 2026-02-01 00:00:00 (GMT). Thus, I downloaded weather forecasts of air temperature 2 meters above the ground and incoming solar radiation for the 0.25° grid that the Grange Creek water temperature is being measured that also started at 2026-02-01 00:00:00 (GMT).

Here are those forecasts. The go 7 days at an hourly time step into the future. 

Air temperature forecast
![]({{ '/assets/img/2026-02-01_MET_forecasts_TEMP.png' | relative_url }})

Solar radiation forecast
![]({{ '/assets/img/2026-02-01_MET_forecasts_SUN.png' | relative_url }})



Here's a table:

| Number | Next number | Previous number |
| :------ |:--- | :--- |
| Five | Six | Four |
| Ten | Eleven | Nine |
| Seven | Eight | Six |
| Two | Three | One |

You can use [MathJax](https://www.mathjax.org/) to write LaTeX expressions. For example:
When \\(a \ne 0\\), there are two solutions to \\(ax^2 + bx + c = 0\\) and they are $$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$

How about a yummy crepe?

![Crepe](https://beautifuljekyll.com/assets/img/crepe.jpg)

It can also be centered!

![Crepe](https://beautifuljekyll.com/assets/img/crepe.jpg){: .mx-auto.d-block :}

Here's a code chunk:

~~~
var foo = function(x) {
  return(x + 5);
}
foo(3)
~~~

And here is the same code with syntax highlighting:

```javascript
var foo = function(x) {
  return(x + 5);
}
foo(3)
```

And here is the same code yet again but with line numbers:

{% highlight javascript linenos %}
var foo = function(x) {
  return(x + 5);
}
foo(3)
{% endhighlight %}

## Boxes
You can add notification, warning and error boxes like this:

### Notification

{: .box-note}
**Note:** This is a notification box.

### Warning

{: .box-warning}
**Warning:** This is a warning box.

### Error

{: .box-error}
**Error:** This is an error box.

## Local URLs in project sites {#local-urls}

When hosting a *project site* on GitHub Pages (for example, `https://USERNAME.github.io/MyProject`), URLs that begin with `/` and refer to local files may not work correctly due to how the root URL (`/`) is interpreted by GitHub Pages. You can read more about it [in the FAQ](https://beautifuljekyll.com/faq/#links-in-project-page). To demonstrate the issue, the following local image will be broken **if your site is a project site:**

![Crepe](/assets/img/crepe.jpg)

If the above image is broken, then you'll need to follow the instructions [in the FAQ](https://beautifuljekyll.com/faq/#links-in-project-page). Here is proof that it can be fixed:

![Crepe]({{ '/assets/img/crepe.jpg' | relative_url }})

<details markdown="1">
<summary>Click here!</summary>
Here you can see an **expandable** section
</details>
