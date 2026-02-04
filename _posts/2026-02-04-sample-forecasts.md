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

{: .box-success}
This is a demo on how forecast the most important aspect of water... temperature. We will go through an exercise that generates 7-day ahead water temperature forecasts for Grange Creek in Thornton, CO. It is a very small, heavily urbanized, stream that sits just behind my home. My daughter love to play in it after school. 
I strongly encourage you to [take review all of the code in Github](https://github.com/ryanmclake/grangeCreekTempForecasts).

**So how does a forecasting workflow work?**

## Let's start with what we know

We know some simple rules of water physics, and I mean let's start really simple here.
+ Water has a high specific heat capacity—it absorbs a lot of heat as energy before it begins to get hot.
+ When it does get hot, it can remain hot for a while before cooling down.
+ My home in Denver, CO USA has seasons (summer, fall, winter, and spring). In winter, the water temperature is colder because the air temperature is cold and we get less sun. 
+ In summer, the water temperature is warmer because it is warmer outside because the air temperature is warmer and we get more sunlight. 

With this very simple thought experiment. We can infer that the temperature in our stream may depend on the temperature of the air.

**Let's forecast water temperature using air temperature and see**



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
