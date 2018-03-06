---
date: '2014-10-14'
title: Twitter Archeology of the Learning Analytics Community
categories: blog
tags:
- analytics
- r
- twitter
- data mining
- visualization
comments: true
summary: To uncover new insights about the learning analytics community by analyzing Twitter archives from the past four LAK conferences.
---

Learning analytics as a nascent field of scholarship is evolving rapidly and garnering broad interest in both educational research and practice. Since the inaugural Learning Analytics and Knowledge (LAK) conference in 2011, exciting moves have been made during the past four years. The Society of Learning Analytics Research (SoLAR) was launched in 2012; the Learning Analytics Summer Institute (LASI) was first held in 2013; the first issue of the Journal of Learning Analytics was published in 2014. After having its own professional organization, annual gatherings, and academic journal, I think it is fair to say learning analytics has established itself as an independent field of study.

In preparation for [LAK15](http://lak15.solaresearch.org), two colleagues and I played with an idea of **mining Twitter archives from the past LAK conferences to uncover insights about the community**. We call this work **Twitter Archeology**. Thanks to [Martin Hawksey](https://twitter.com/mhawksey)'s amazing [Twitter Archiving Google Sheet](http://tags.hawksey.info/) (TAGS; which is in its 6th version right now), we were able to access and compile a (hopefully) complete set of tweets from the past four LAK conferences. We played with a bunch of analysis, including basic descriptive analysis, interaction (social) network analysis, hashtag analysis and topic modeling, and were able to find some interesting results to report. In this blog post, I would like to briefly share two findings that I think are pretty interesting.

### The Flow of the LAK Community

To understand the composition of the LAK community as reflected by Twitter participation, we tracked participation of all Twitter participants over the years, focusing on new and returning people each year. The results are visualized as a Sankey diagram below. In this diagram, the horizontal axis represents the time dimension, with each column representing one conference. The fifth (or last) column represents participants who stopped participating at some point -- in other words, those who "left" the community. Within each column, new and returning participants are presented separately. In the diagram, all lines are drawn from left to right, representing the flow of participants from one section to another between two columns; the width of a line denotes the volume of its flow.

![Sankey Diagram](/assets/sankey.png)

To our surprise, **only a small fraction of participants have been returning to LAK conferences' Twitter discussion**, indicated by the thinner lines towards the "Back" sections of LAK12 to LAK14. By looking at the returning participants more closely, we found that only 18 colleagues (among all 1,217 unique participants) participated in Twitter discussion during all LAK conferences. This number only increased to 55 when we counted users participating at least three conferences. Overall, the majority of participants only participated in one conference and never returned. The LAK community seems to be "fluid" reflected by Twitter participation during its annual conferences. While it keeps attracting interested people from various domains, the community is still more or less unstable as an emerging field of research and practice.

### Evolution of Research Topics

In addition to tracking users, we were also interested in tracking research topics, especially because learning analytics is such a new field with various research interests emerging all the time. So we applied [latent Dirichlet allocation (LDA)](http://en.wikipedia.org/wiki/Latent_Dirichlet_allocation), which [I had some opportuniticies to play with  before](http://meefen.github.io/blog/2013/07/01/topic-modeling-and-visualization-of-knowledge-forum-discussion/), to uncover underlying topics in Twitter discussion during LAK conferences. We thought this could somehow complement previous analysis of learning analytics literature in recent [LAK Data Challenges](http://lak.linkededucation.org) because not everything has made it into the literature yet and not everyone having an interest in learning analytics would necessarily want to publish.

After some fine-tuning of LDA, we were pretty happy with a 34-topic model. After exploring each individual topic and its top terms with the amazing [LDAvis](https://github.com/cpsievert/LDAvis) R package, we found **tweet topics generally fell into a few distinguishable categories**, including (1) information-sharing related to conferences and the community (e.g., sessions, workshops, slides), (2) experience-sharing and comments (e.g., "how much someone loved a study"), and (3) specific research topics (such as MOOC, assessment, students, course design). We further tagged each topic with its pertinent terms and then focused on topics most relevant to learning analytics research in order to track their evolution over the years.

![Topic Evolution](/assets/track_topics.png)

The line chart above illustrates the change of eleven selected topics. The x-axis represents *year*; the y-axis represents the percentage of a topic in a year's tweets. As a validity check, two topics popular in LAK14 are included: Topic 10 {social use media win networks share survey ipad} was related to a promoted project and Topic 11 {graesser systems predictive agents model tutors} was about a keynote speech. These two topics both peeked during LAK14, showing a certain level of validity of our LDA model.

Further inspection of the topics identified **an increasing emphasis on students, need, assessment, and feedback in the community**, indicated by the growing popularity of Topics 1-4. The popularity of student-related topics seemed to agree with previous topic modeling of LAK publications ([pdf](http://ceur-ws.org/Vol-974/lakdatachallenge2013_08.pdf)), although previous work didn't look at the trend. In addition, each year's conference presented unique hot topics:

- Topics relevant to ethics and social media were relatively popular at LAK11
- Big data, linked data, and educational data mining were trending at LAK12
- Course design, ethical issues, discourse, and measurement were popular during LAK13
- Topics involving assessment, student needs, intelligent tutors, and educational data mining were rising at LAK14

Not sure how much the results reflect the real experience of the attendees. In case you were one of them, please do share your thoughts.

### Reflections

No matter whether it is generally helpful or systematically flawed, Twitter analytics has revealed some interesting phenomena about the community. The biggest challenge of this work, and also one criticism I expect from reviewers, is that because not all conference participants or community members use Twitter, the analysis of tweets could only reconstruct parts of the dialogues and would run the risk of missing important messages, events, or figures. Someone may also very well question whether people gathering around a Twitter hashtag could be treated as a "community" at all -- if we apply a higher standard for a community. As a matter of fact, because of the unique information diffusion mechanism of Twitter, people who were peripheral in the network might only retweeted something from an influential figure. Should we count her as a "community member" at all? Those are all valid worries I currently do not have a good response to. Maybe if we connect tweets and academic publications (and maybe people's blogs), we would be able to construct a more integrated picture of the learning analytics community.

To find more about the work, read [our paper](http://meefen.github.io/public/files/Chen_LAK15_Twitter_Archeology.pdf) published in the LAK15 proceedings.
