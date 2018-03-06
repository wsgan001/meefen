---
date: '2013-07-01'
title: Topic Modeling and Visualization of Knowledge Forum Discussion
categories:
- blog
tags:
- analytics
- semantic analysis
published: true
---

In an earlier [blog post](http://bodongchen.com/blog/?p=301) I played
with the idea of visualizing Knowledge Forum discourse in a 2D space, to
support one specific perspective of community knowledge focusing on
semantic similarity/distance among contributions. I used [Latent
Semantic Analysis](http://lsa.colorado.edu/whatis.html) (LSA) for
similarity computation and [Multidimensional
scaling](http://en.wikipedia.org/wiki/Multidimensional_scaling) (MDS)
for dimensionality reduction. The results was interesting, with notes
around a same topic generally clustered together. However, as one
colleague pointed out in a comment, it's hard to interpret topics around
different clusters and it would be nice if it's possible to inspect
clusters and somehow label them.

At the [CSCL 2013 conference](http://cscl2013.isls.org/) around ten days
ago I attended an interactive presentation by Norma Ming. In her work,
she conducted [probabilistic
LSA](http://en.wikipedia.org/wiki/Probabilistic_latent_semantic_analysis)
(pLSA) on four weeks of online discussion by college students in a
biology class and extracted 100 topics for the dataset. After pLSA, the
semantic space of the online discussion could be represented by a
100-dimensional space, with each post represented by a 100-dimensional
vector. To visualize all posts on a 2D space, locally linear embedding
(LLE) was further conducted, reducing the 100-dimensional space to 2D
while keeping locally clustered posts in the high dimensional space
still close in the 2D space. With posts visualized in a 2D canvas, Norma
further mapped students' scores of the final exam as well as week \# of
discussion onto the visualization. Interestingly, they found students
achieving higher scores tended to contribute more posts in "outer
space", while low-achieving students' posts only covered the central
area. With course week information, they found quite clear boundaries
among discussion of different weeks, although over-plotting might be an
issue as you see in the following figure from their paper. These results
were pretty powerful, especially if we don't only think retrospectively
but also prospectively. For example, whether is it possible to guide
students to "outer space" by progressively represent their discussion in
this way to encourage "metadiscourse" (namely, discourse about
discourse)?

![norma](https://dl.dropboxusercontent.com/u/7599158/wp/figure/norma-plsa.png)

Coming back from CSCL, I resumed the work of representing semantic space
of Knowledge Forum discussion for metadiscourse. Rather than using pLSA,
I used [latent Dirichlet
allocation](https://en.wikipedia.org/wiki/Latent_Dirichlet_allocation)
(LDA), a more sophisticated technique for topic modeling. The key idea
is similar to Norma's work, which is to represent discourse in a
high-dimensional space and then reduce it to 2D for visualization. [A
Shiny app](http://glimmer.rstudio.com/bodong/topicmodels) was developed
as a proof of concept. It has three main functionalities:

I. Visualization of semantic space. The visualization is implemented
with a Google ("non-moving Motion") Chart, which allows users to
interact with the visualization. Users can easily change x and y axises
as well as the meaning of color and size of dots in the visualization to
help interpret the results. It provides a potentially powerful way to
interact with data if the data have a rich set of variables. Further,
zooming in functionality is available if an area is cluttered with too
many dots so the problem of over-plotting could be alleviated.

![topicmodels
visualization](https://dl.dropboxusercontent.com/u/7599158/wp/figure/topicmodels-vis.png)

​II. Summary of extracted topics. Top words of each extracted topic are
listed to help users interpret the results. Users can choose to show
more (or less) top words in the process of making sense of a topic.
Moreover, numbers of notes under topics are also provided, to help
identify popular topics. It opens the door to further tracking
popularity of topics in a discussion.

![topicmodels
topics](https://dl.dropboxusercontent.com/u/7599158/wp/figure/topicmodels-topics.png)

​III. Detailed content of notes. Detailed content of notes are also
presented for users to make sense of the results and to decide whether
the topic modeling results are accurate.

![topicmodels
notes](https://dl.dropboxusercontent.com/u/7599158/wp/figure/topicmodels-notes.png)

This application is a first step of my exploration of visualizing
students' online discourse to facilitate metadiscourse. I plan to
introduce more variables such as authorship, timestamp, and various
types of coding results into this visualization in the future. **Please
let me know if you wish to explore any idea.**
