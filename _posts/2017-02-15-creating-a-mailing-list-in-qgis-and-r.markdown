---
author: realdataweb
comments: true
date: 2017-02-15 17:18:14+00:00
layout: post
link: https://realdataweb.wordpress.com/2017/02/15/creating-a-mailing-list-in-qgis-and-r/
slug: creating-a-mailing-list-in-qgis-and-r
title: Creating a Mailing List in QGIS and R
wordpress_id: 128
categories:
- Programming
- R
tags:
- '2017'
- data science
- GIS
- Programming
- R
- Raleigh
---

My day job as a real estate agent requires a myriad of skills, ranging from accounting to negotiation to business analysis.  Frequently (about every three months) I whip out my marketing skills to advertise [my business.](https://www.facebook.com/realest8agent/)  This time I decided to send out postcards to an entire neighborhood in which I had sold homes recently.  Typically, agents will buy a mail route from the post office and hand over their postcards.  In the spirit of frugality and proving a point, I cracked my knuckles and went hunting for data.

**Get the shapefiles.  **[Wake County Open Data](http://data-wake.opendata.arcgis.com/) (or your local open data hub) has a wealth of county-level data including subdivision boundaries and individual address points.  Download both shapefiles and  load them into your favorite [GIS program](http://www.qgis.org/en/site/about/index.html).  This step can probably be done in R, but I find using QGIS fairly intuitive and much faster at plotting large shapefiles.


![Screen Shot 2017-02-15 at 11.07.05 AM.png](https://realdataweb.files.wordpress.com/2017/02/screen-shot-2017-02-15-at-11-07-05-am.png)     ![Screen Shot 2017-02-15 at 11.10.33 AM.png](https://realdataweb.files.wordpress.com/2017/02/screen-shot-2017-02-15-at-11-10-33-am.png)




**Filter the addresses.  **After loading the address and subdivision shapefiles into QGIS, clip the address shapefile using the subdivision shapefile to save the addresses of interest in a new layer.  Save that puppy as a .csv and we can load it up in R.


![Screen Shot 2017-02-15 at 11.24.11 AM.png](https://realdataweb.files.wordpress.com/2017/02/screen-shot-2017-02-15-at-11-24-11-am.png?w=368)

**Manipulate in R.  **Now we've got the info we want.  A few lines of code will give us something the post office (or Excel) will understand.

![screen-shot-2017-02-15-at-11-35-42-am](https://realdataweb.files.wordpress.com/2017/02/screen-shot-2017-02-15-at-11-35-42-am.png)

[code language="R"]walden_creek <- read_csv("~/Desktop/walden creek.csv")
attach(walden_creek)
adds <- paste(FULLADDR, POSTAL_CIT, "NC", "27523", sep = ",")
detach(walden_creek)
write.table(adds, "adds.csv", sep = ",")
[/code]

Short and sweet, but I thought this was an interesting way to use data for a practical purpose.  People seem to be using R in exciting ways these days - if you see any creative, different projects please share.

- Kiefer Smith
