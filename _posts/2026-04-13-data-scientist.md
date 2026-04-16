---
title: "My Data Science Work"
author: "Lee Stanish"
subtitle: Data science projects
gh-repo: https://github.com/lstanish-usgs
tags: data-science, hydrology, water-quality
comments: true
mathjax: true
layout: post
cover-img: /assets/img/hyswap_streamflow_duration_hydrograph_ex11.png
thumbnail-img: /assets/img/hyswap_streamflow_duration_hydrograph_ex11.png
share-img: /assets/img/hyswap_streamflow_duration_hydrograph_ex11.png
---


### [metScanR](https://www.rdocumentation.org/packages/metScanR/versions/1.2.3)

This R package helps users find, map and gather environmental data and metadata from monitoring sites globally.

Users can search for and filter metadata from > 157,000 environmental monitoring stations among 219 countries/territories and >20 networks/organizations via elevation, location, active dates, elements measured (e.g., temperature, precipitation), country, network, and/or known identifier. 

I was excited to cut my teeth with R package development on this package, which was the brain child of former NEON colleague [Josh Roberti] (https://github.com/jaroberti/metScanR).


### [datRetrieval](https://doi-usgs.github.io/dataRetrieval/index.html)

![]({{ '/assets/img/dataRetrieval_hex_logo.png' | relative_url }})

The [`dataRetrieval`](https://github.com/DOI-USGS/dataRetrieval/) package was created to simplify the process of loading hydrologic data into the R environment. It is designed to retrieve the major data types of U.S. Geological Survey (USGS) hydrology data that are available on the web, as well as data from the Water Quality Portal (WQP), which houses hundreds of millions of water quality data records from the US Environmental Protection Agency (EPA) [STORET](https://www.epa.gov/waterdata/water-quality-data) database.

With over 5,000 downloads *every month*, this popular package helps water resource managers, hydrologists, and water quality specialists streamline their data aggregation workflows for tasks such as running automated analyses and creating real-time dashboards. It also comes with excellent tutorials and documentation, which has allowed the package to become a popular teaching tool for students to learn fundamental data science skills and become proficient in managing 'big data' sets.

As Product Owner for `dataRetrieval`, I helped navigate the package through a massive data restructuring event that occurred for USGS and EPA data streams. With such a large and diverse user base, we put a ton of forethought and planning into carrying out package updates to minimuze disruptions to users and to make the transition to new data structures as painless as possible. We had a strong public outreach campaign to keep users up to date and informed during this period, including a [Status](https://doi-usgs.github.io/dataRetrieval/articles/Status.html) page, blog posts, and public webinars.


### [hySwap] (https://doi-usgs.github.io/hyswap/)

hyswap (HYdrologic Surface Water Analysis Package) is a Python package that provides a set of functions for manipulating and visualizing USGS water data. It provides functions for calculating statistics (e.g., exceedance probabilities, daily historic percentiles) and generating plots such as flow duration curves and streamflow duration hydrographs.

I served as Product Owner during the development and release of this package. This was my first time with a Python package and I learned a lot about the  package release process. One of my primary objectives for the package was to create extensive and high-quality documentation. In today's world requiring data literacy, it was critical that we reduce the barrier to entry for newer Python users by creating great documentation, including ready-to-use Jupyter notebooks with examples of the most common analyses to get new users started quickly.

Regional runoff calculations
![]({{ '/assets/img/hyswap_regional_runoff_calculations_24.png' | relative_url }})

Flow duration hydrographs
![]({{ '/assets/img/hyswap_streamflow_duration_hydrograph_ex9.png' | relative_url }})

![]({{ '/assets/img/hyswap_streamflow_duration_hydrograph_ex11.png' | relative_url }})

Stream flow conditions (percentile calculations)
![]({{ '/assets/img/hyswap_VisStreamflowConditions.png' | relative_url }})
