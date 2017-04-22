---
author: realdataweb
comments: true
date: 2017-03-04 15:33:53+00:00
layout: post
link: https://realdataweb.wordpress.com/2017/03/04/mapping-happiness-and-isoline-functions/
slug: mapping-happiness-and-isoline-functions
title: Mapping Happiness and Isoline Functions
wordpress_id: 258
categories:
- Text
tags:
- data
- GIS
- happiness
- maps
- Programming
---

![heart-of-texas-hot-air-balloon](https://realdataweb.files.wordpress.com/2017/03/heart-of-texas-hot-air-balloon.jpg)

Most of the time I get emails they're either work-related or spam-related.  Sometimes the spam turns out to be interesting.  About once a month I'll get a digest of articles from [Teleport](https://teleport.org/) .  This month there was an [article from Forbes](http://bit.ly/2mBp18B) about mapping global happiness using news headlines.  I'm assuming the author used natural language processing of some sort, as he mentions evaluating the context in which each location is written about ( sentiment analysis).

Not entirely sure how accurate the methodology is (and the final product is somewhat hard to draw conclusions from), but it's a super cool concept nonetheless.  Unfortunately, the author did not leave us with a GitHub repo to pore through, but did mention making use of Google's BigQuery platform and Carto's mapping system.

Being the fantastic procrastinator that I am, I took a look at Carto's services.  Turns out they [have a pretty cool feature (with an API)](https://carto.com/location-data-services/isolines) that creates time and distance isolines.  Might try using something like that in an upcoming project.  Stay tuned!  Or check out my [GitHub](https://github.com/kiefersmith) for a sneak peek.
