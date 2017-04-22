---
author: realdataweb
comments: true
date: 2017-04-22 11:52:14+00:00
excerpt: '<p>In real estate, spatial data is the name of the game. Countless other
  domains utilize the power of this data, which is becoming more prevalent by the
  day. In this post I will go over a few simple, but powerful tools to get you started
  using using geographic information in R. GISTools provides an easy-to-use [&hellip;]</p>

  '
layout: post
link: https://realdataweb.wordpress.com/2017/04/22/using-r-as-a-gis/
slug: using-r-as-a-gis
title: Using R as a GIS
wordpress_id: 516
tags:
- '2017'
- analysis
- data
- data science
- GIS
- graph
- map
- maps
- Programming
- R
- Rmarkdown
- visualization
---

![1](https://realdataweb.files.wordpress.com/2017/04/1.jpg)

In real estate, spatial data is the name of the game. Countless programs
in other domains utilize the power of this data, which is becoming more
prevalent by the day.

In this post I will go over a few simple, but powerful tools to get you
started using using geographic information in R.

[code lang="r"]
##First, some libraries##
#install.packages('GISTools', dependencies = T)
library(GISTools)
[/code]

`GISTools` provides an easy-to-use method for creating shading schemes
and choropleth maps. Some of you may have heard of the `sp` package,
which adds numerous spatial classes to the mix. There are also functions
for analysis and making things look nice.

Let's get rolling: source the `vulgaris` dataset, which contains
location information for Syringa Vulgaris (the Lilac) observation
stations and US states. This code plots the states and `vulgaris`
points.

[code lang="r"]
data(&quot;vulgaris&quot;) #load data
par = (mar = c(2,0,0,0)) #set margins of plot area
plot(us_states)
plot(vulgaris, add = T, pch = 20)
[/code]

![alt text](https://thepracticaldev.s3.amazonaws.com/i/23vc4dmomjg5xns25ygk.png)

One thing to note here is the structure of these objects. `us_states` is
a SpatialPolygonsDataFrame, which stores information for plotting shapes
(like a shapefile) within its attributes. `vulgaris` by contrast is a
SpatialPointsDataFrame, which contains data for plotting individual
points. Much like a `data.frame` and `$`, these objects harbor
information that can be accessed via `@`.

[code lang="r"]
kable(head(vulgaris@data))
[/code]

<table >

<tr >
  
  Station
  Year
  Type
  Leaf
  Bloom
  Station.Name
  State.Prov
  Lat
  Long
  Elev
</tr>

<tbody >
<tr >
  
<td >3695
</td>
  
<td align="right" >61689
</td>
  
<td align="right" >1965
</td>
  
<td align="left" >Vulgaris
</td>
  
<td align="right" >114
</td>
  
<td align="right" >136
</td>
  
<td align="left" >COVENTRY
</td>
  
<td align="left" >CT
</td>
  
<td align="right" >41.8
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >146
</td>
</tr>
<tr >
  
<td >3696
</td>
  
<td align="right" >61689
</td>
  
<td align="right" >1966
</td>
  
<td align="left" >Vulgaris
</td>
  
<td align="right" >122
</td>
  
<td align="right" >146
</td>
  
<td align="left" >COVENTRY
</td>
  
<td align="left" >CT
</td>
  
<td align="right" >41.8
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >146
</td>
</tr>
<tr >
  
<td >3697
</td>
  
<td align="right" >61689
</td>
  
<td align="right" >1967
</td>
  
<td align="left" >Vulgaris
</td>
  
<td align="right" >104
</td>
  
<td align="right" >156
</td>
  
<td align="left" >COVENTRY
</td>
  
<td align="left" >CT
</td>
  
<td align="right" >41.8
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >146
</td>
</tr>
<tr >
  
<td >3698
</td>
  
<td align="right" >61689
</td>
  
<td align="right" >1968
</td>
  
<td align="left" >Vulgaris
</td>
  
<td align="right" >97
</td>
  
<td align="right" >134
</td>
  
<td align="left" >COVENTRY
</td>
  
<td align="left" >CT
</td>
  
<td align="right" >41.8
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >146
</td>
</tr>
<tr >
  
<td >3699
</td>
  
<td align="right" >61689
</td>
  
<td align="right" >1969
</td>
  
<td align="left" >Vulgaris
</td>
  
<td align="right" >114
</td>
  
<td align="right" >138
</td>
  
<td align="left" >COVENTRY
</td>
  
<td align="left" >CT
</td>
  
<td align="right" >41.8
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >146
</td>
</tr>
<tr >
  
<td >3700
</td>
  
<td align="right" >61689
</td>
  
<td align="right" >1970
</td>
  
<td align="left" >Vulgaris
</td>
  
<td align="right" >111
</td>
  
<td align="right" >135
</td>
  
<td align="left" >COVENTRY
</td>
  
<td align="left" >CT
</td>
  
<td align="right" >41.8
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >146
</td>
</tr>
</tbody>
</table>

Let's take a look at some functions that use this data.

[code lang="r"]
newVulgaris kable(head(data.frame(newVulgaris)))
[/code]

<table >

<tr >
  
  x
  y
</tr>

<tbody >
<tr >
  
<td >3 4896
</td>
  
<td align="right" >-67.65
</td>
  
<td align="right" >44.65
</td>
</tr>
<tr >
  
<td >3 4897
</td>
  
<td align="right" >-67.65
</td>
  
<td align="right" >44.65
</td>
</tr>
<tr >
  
<td >3 4898
</td>
  
<td align="right" >-67.65
</td>
  
<td align="right" >44.65
</td>
</tr>
<tr >
  
<td >3 4899
</td>
  
<td align="right" >-67.65
</td>
  
<td align="right" >44.65
</td>
</tr>
<tr >
  
<td >3 4900
</td>
  
<td align="right" >-67.65
</td>
  
<td align="right" >44.65
</td>
</tr>
<tr >
  
<td >3 4901
</td>
  
<td align="right" >-67.65
</td>
  
<td align="right" >44.65
</td>
</tr>
</tbody>
</table>

`gIntersection`, as you may have guessed from the name, returns the
intersection of two spatial objects. In this case, we are given the
points from `vulgaris` that are within `us_states`. However, the rest of
the `vulgaris` data has been stripped from the resulting object. We've
got to jump through a couple of hoops to get that information back.

[code lang="r"]
&lt;br /&gt;newVulgaris &lt;- data.frame(newVulgaris)
tmp &lt;- rownames(newVulgaris)
tmp &lt;- strsplit(tmp, &quot; &quot;)
tmp &lt;- (sapply(tmp, &quot;[[&quot;, 2))
tmp &lt;- as.numeric(tmp)
vdf &lt;- data.frame(vulgaris)
newVulgaris &lt;- subset(vdf, row.names(vdf) %in% tmp)
[/code]

<table >

<tr >
  
  Station
  Year
  Type
  Leaf
  Bloom
  Station.Name
  State.Prov
  Lat
  Long
  Elev
  Long.1
  Lat.1
  optional
</tr>

<tbody >
<tr >
  
<td >3695
</td>
  
<td align="right" >61689
</td>
  
<td align="right" >1965
</td>
  
<td align="left" >Vulgaris
</td>
  
<td align="right" >114
</td>
  
<td align="right" >136
</td>
  
<td align="left" >COVENTRY
</td>
  
<td align="left" >CT
</td>
  
<td align="right" >41.8
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >146
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >41.8
</td>
  
<td align="left" >TRUE
</td>
</tr>
<tr >
  
<td >3696
</td>
  
<td align="right" >61689
</td>
  
<td align="right" >1966
</td>
  
<td align="left" >Vulgaris
</td>
  
<td align="right" >122
</td>
  
<td align="right" >146
</td>
  
<td align="left" >COVENTRY
</td>
  
<td align="left" >CT
</td>
  
<td align="right" >41.8
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >146
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >41.8
</td>
  
<td align="left" >TRUE
</td>
</tr>
<tr >
  
<td >3697
</td>
  
<td align="right" >61689
</td>
  
<td align="right" >1967
</td>
  
<td align="left" >Vulgaris
</td>
  
<td align="right" >104
</td>
  
<td align="right" >156
</td>
  
<td align="left" >COVENTRY
</td>
  
<td align="left" >CT
</td>
  
<td align="right" >41.8
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >146
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >41.8
</td>
  
<td align="left" >TRUE
</td>
</tr>
<tr >
  
<td >3698
</td>
  
<td align="right" >61689
</td>
  
<td align="right" >1968
</td>
  
<td align="left" >Vulgaris
</td>
  
<td align="right" >97
</td>
  
<td align="right" >134
</td>
  
<td align="left" >COVENTRY
</td>
  
<td align="left" >CT
</td>
  
<td align="right" >41.8
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >146
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >41.8
</td>
  
<td align="left" >TRUE
</td>
</tr>
<tr >
  
<td >3699
</td>
  
<td align="right" >61689
</td>
  
<td align="right" >1969
</td>
  
<td align="left" >Vulgaris
</td>
  
<td align="right" >114
</td>
  
<td align="right" >138
</td>
  
<td align="left" >COVENTRY
</td>
  
<td align="left" >CT
</td>
  
<td align="right" >41.8
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >146
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >41.8
</td>
  
<td align="left" >TRUE
</td>
</tr>
<tr >
  
<td >3700
</td>
  
<td align="right" >61689
</td>
  
<td align="right" >1970
</td>
  
<td align="left" >Vulgaris
</td>
  
<td align="right" >111
</td>
  
<td align="right" >135
</td>
  
<td align="left" >COVENTRY
</td>
  
<td align="left" >CT
</td>
  
<td align="right" >41.8
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >146
</td>
  
<td align="right" >-72.35
</td>
  
<td align="right" >41.8
</td>
  
<td align="left" >TRUE
</td>
</tr>
</tbody>
</table>

Look familiar? Now we've got a data frame with the clipped `vulgaris`
values and original data preserved.

[code lang="r"]
vulgarisSpatial ```

After storing our clipped data frame as a SpatialPointsDataFrame, we can
again make use of it - in this case we add a shading scheme to the
`vulgaris` points.

``` r
shades shades$cols plot(us_states)
choropleth(vulgarisSpatial, vulgarisSpatial$Elev,shading = shades, add = T, pch = 20)
[/code]

![alt text](https://thepracticaldev.s3.amazonaws.com/i/l6hm6mnpkdlc1yo04nzd.png)

Colors are pretty, but what do they mean? Let's add a legend.

[code lang="r"]
us_states@bbox #Get us_states bounding box coordinates.
[/code]


    
     ##min max
     ## r1 -124.73142 -66.96985
     ## r2 24.95597 49.37173



[code lang="r"]
plot(us_states)
choropleth(vulgarisSpatial, vulgarisSpatial$Elev,shading = shades, add = T, pch = 20)
par(xpd=TRUE) #Allow plotting outside of plot area.
choro.legend(-124, 30, shades, cex = .75, title = &quot;Elevation in Meters&quot;) # Plot legend in bottom left. Takes standard legend() params.
[/code]

![alt text](https://thepracticaldev.s3.amazonaws.com/i/1g2o2k4xei3rwkxjnpfc.png)

It looks like there's a lot going on in the Northeastern states. For a
closer look, create another clipping (like above) and plot it. Using the
structure below, we can create a selection vector. I have hidden the
full code since it is repetitive (check [GitHub](https://github.com/kiefersmith/WordpressMD) for the full code.)

[code lang="r"]
index '...'
[/code]

[code lang="r"]
plot(us_states[index,])
choropleth(vulgarisNE, vulgarisNE$Elev,shading = shades, add = T, pch = 20)
par(xpd = T)
choro.legend(-73, 39.75, shades, cex = .75, title = &quot;Elevation in Meters&quot;)
[/code]

![alt text](https://thepracticaldev.s3.amazonaws.com/i/fdaheorcg0jr8zq0oepb.png)

Hopefully this has been a useful introduction (or refresher) on spatial
data. I always learn a lot in the process of writing these posts. If you
have any ideas or suggestions please leave a comment or feel free to
[contact me](mailto:kieferisgreat@gmail.com)!

Happy mapping,

Kiefer
