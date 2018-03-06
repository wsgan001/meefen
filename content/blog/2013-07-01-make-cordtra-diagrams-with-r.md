---
date: '2013-07-01'
title: Make CORDTRA Diagrams with R
categories:
- blog
tags:
- learning analytics
- visualization
published: true
---

CORDTRA (Chronologically-Ordered Representation of Discourse and
Tool-Related Activity) is a visualization technique proposed by Cindy
Hmelo-Silver (2003) for interpreting collaborative learning processes,
based on Luckin et al.'s CORDFU (Chronologically-Ordered Representation
of Discourse and Features Used). This technique could provide a holistic
view of learning processes by making temporal relationship among various
types of learning activities visible. By presenting a few interesting
case studies, Hmelo-Silver and colleagues (2003, 2008) demonstrate that
CORDTRA could provide useful insights about student interactions in
computer-supported collaborative learning (CSCL).

Detailed description of CORDTRA could be found in Hmelo-Silver and her
colleagues' articles. The general idea of this visualization is to first
sort discourse units chronologically and put them on an X axis, and then
map interested coding results (or log information) of discourse onto the
axis, with each coding category represented as a horizontal line. In
this way, researchers could inspect the representation visually and look
for possible relations among discourse events pertinent to their
research questions. Here is an example of a CORDTRA diagram:

![CORDTRA
example](http://origin-ars.els-cdn.com/content/image/1-s2.0-S0360131503000812-gr3.jpg)

CORDTRA Shiny App
-----------------

Working on data analysis of my doctoral research, which involves various
types of student activities in Knowledge Forum, I decided to give this
technique a try. According to Cindy, they used Excel to create CORDTRA
diagrams. They could zoom into a timeline to study events around a
certain period of time in detail. This is pretty handy! But at the same
time I heard complains about the complexity of the task of creating a
CORDTRA diagram from colleagues who incorporated it in their research. I
could imagine that customizing shapes of dots in an Excel diagram is not
always easy.

Inspired by a [blog post](http://www.nise81.com/archives/2202) about
creating CORDTRA diagrams with D3.js, I thought it might be a good idea
to develop a simple R-based program that could effortlessly convert
coded CSCL data into a CORDTRA diagram. So here we are, [a Shiny
app](http://glimmer.rstudio.com/bodong/CORDTRA-R) (based on R) for
creating CORDTRA diagrams.

What this app asks for is only a spreadsheet containing sorted discourse
units and their coding results. The first few lines of the spreadsheet I
use for demo look like the following:

![CORDTRA
diagram](https://dl.dropboxusercontent.com/u/7599158/wp/figure/cordtra-data.png)

The first column of the table contains indices of discourse units. (In
my case, discourse units are Knowledge Forum notes.) The other four
columns contain coding results of four coding schemes, including *Ways
of contributing*, *Levels of problems*, *Scientific sophistication*, and
*Epistemic complexity*. They are categorical or ordinal data, with each
category or level of them representing a certain interested event in my
research.

With [the Shiny app](http://glimmer.rstudio.com/bodong/CORDTRA-R/) I've
developed, this table can be automatically transformed to a CORDTRA
diagram like below. In this diagram, each coding scheme, which maps to
each table column, has a distinctive color, and each category under a
coding scheme is represented by a specific shape.

![CORDTRA
diagram](https://dl.dropboxusercontent.com/u/7599158/wp/figure/cordtra.png)

This app also allows researchers to zoom in/out the diagram by selecting
range of discourse units to be visualized. It also enables researchers
to filter certain coding categories by deselecting them on the left
panel.

Steps further
-------------

There are many way to interpret a CORDTRA visualization. Beside visual
interpretation, one analysis researchers may wish to do is to check
co-occurrence of certain types of events. To facilitate this analysis,
this Shiny app extracts a co-occurrence matrix of all coding categories,
and visualize it as a force-directed map (see below). The following
visualization may not be the best example to show the power of this
functionality, because the only fruitfulness of it is showing that we've
coded *scientific sophistication* and *complexity* for *theorizing*
notes and *depth of questions* for *questioning* notes. But if you have
a richer set of coding schemes, interesting patterns which are hard to
inspect in CORDTRA may become visible in the visualization of
co-occurrence.

![CORDTRA
map](https://dl.dropboxusercontent.com/u/7599158/wp/figure/cordtra-cooccurrence.png)

Another direction I wish to take is to make this diagram more
interactive. Thanks to the googleVis R package, it becomes possible to
integrate Google Charts into a Shiny app. I started by playing with the
Google Motion Chart---a cool visualization that could show change of
objects overtime. Probably the most famous example of this visualization
is [Hans Rosling's TED
talk](http://www.ted.com/talks/hans_rosling_reveals_new_insights_on_poverty.html)
about poverty and world economy. In this app, because I don't have
enough numeric data to feed to x and y axises, it could only track
accumulated occurrence of each coding category. If student/author
information of each discourse unit is available, it might become
possible to create aggregated information around students to visualize
and compare certain aspect of discourse performance of all students.

![motion
chart](https://dl.dropboxusercontent.com/u/7599158/wp/figure/cordtra-motion.png)

References
----------

-   Hmelo-Silver, C. E. (2003). Analyzing collaborative knowledge
    construction. *Computers & Education, 41(4)*, 397–420.
    doi:10.1016/j.compedu.2003.07.001
-   Hmelo-Silver, C. E., Chernobilsky, E., & Jordan, R. (2008).
    Understanding collaborative learning processes in new learning
    environments. *Instructional Science, 36(5-6)*, 409–430.
    doi:10.1007/s11251-008-9063-8
-   Luckin, R., Plowman, L., Laurillard, D., Stratfold, M., Taylor, J.,
    & Corben, S. (2001). Narrative evolution: learning from students’
    talk about species variation. *International Journal of AI in
    Education, 12*, 100–123.
