---
date: '2013-04-03'
title: KNAER Data Visualization Workshop
categories:
- blog
tags:
- data visualization
published: true
---

Today I was attending [a data visualization
workshop](http://www.knaer-recrae.ca/knowledge-mobilization/events/item/161-seeing-what-is-before-us-the-use-of-data-visualization)
organized by the KNAER Data Visualization project in collaboration with
[AERO](http://www.aero-aoce.org/). I was one of the presenters,
including Paul Anisef, Rob Brown, [Chris Conley](http://cconley.ca/) and
Cosmin Marmureanu. It was the first time I met with them in person
although we have been working together for a few months already on data
visualization.

The workshop went quite well, with around 60 participants mostly from
school boards and the ministry of education. Rob started by introducing
the history of this data visualization project. After that, Chris took
over and gave a nice introduction to a number of important principles of
data visualization. Then he guided everybody working through a few neat
data visualization techinques in Excel, including pyramid chart, slope
chart, thermometer chart, and interactive charts. As a person who mainly
used Excel for bar charts when coming to data visualization, it was
amazing to learn those new techniques.

After the Excel session was done, Cosmin who has been working
extensively on GIS visualization of educational data introduced us to a
few mapping tools including [Google Fusion
Tables](http://www.google.com/drive/start/apps.html#fusiontables),
[ArcGIS](http://www.arcgis.com/) and Quantum GIS. Putting data on top of
maps could become really powerful as I saw at [the Toronto Open Data Day
event](http://bodongchen.com/blog/?p=285) a few weeks ago. Mashing up
educational data on top of maps could provide fresh ways of looking at
the data that cannot be found elsewhere, and could help communicate
information strongly to impact planning and policy making. However,
interpreting information from a map is always tricky and needs special
caution, because there is always rich information behind or attached to
the map and either the presenters or the audience could easily become
biased.

After lunch, I led a session focusing on data visualization with
[R](http://www.r-project.org/). It was the first time I was giving a
presentation solely focusing on R since I learned it last year in a
course on Coursera. It was also the first time to present to an audience
mainly from school boards. So the experience was quite interesting. As
most of the participants were not familiar with R, I tried to make
everything simple and straightforward, building visualizations step by
step by adding one new element each time. The presentation mainly
focused on [ggplot2](http://ggplot2.org/), and briefly mentioned
[Shiny](http://www.rstudio.com/shiny/) and
[knitr](http://yihui.name/knitr/) at the end. By showing what you can do
with only one line of code in R, I was trying to convey how powerful and
flexible R could become especially in exploring data. The demo I did
mainly focused on some ordinary data visualization techniques such as
barplot, boxplot, histogram, and scatterplot. I also included a few
slides about data manipulation and transformation in R as well as more
advanced stuff like heatmaps and geographic maps. After this demo was
done, Chris showed how to make venn diagram and [Google motion
chart](https://developers.google.com/chart/interactive/docs/gallery/motionchart)
in R, which was very cool. I've posted my
[slides](http://bodongchen.com/slides/knaer-workshop/) and
[handout](http://rpubs.com/dirkchen/knaer-workshop) online. (They
themselves were written with R in [this
file](http://bodongchen.com/slides/knaer-workshop/index.Rmd) and
compiled into slides with [Slidify](http://ramnathv.github.com/slidify/)
and to handout with knitr.)

We left the day after Paul wrapped up the workshop discussing future
possibilities of this project and knowledge mobilization work to be
done.
