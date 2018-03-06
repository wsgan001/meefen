---
date: '2014-06-06'
title: 'Knowledge Forum API: A demo'
categories: blog
tags:
- analytics
- knowledge building
comments: true
summary: A demo of using the new Knowledge Forum API to compile knowledge building analytics.
---

[Knowledge Forum (KF)](http://en.wikipedia.org/wiki/Knowledge_Forum) has been recognized as the founding software in the computer-supported collaborative learning (CSCL) community. And it was also one of the earliest to offer embedded analytic tools for formative assessment. Thanks to contributions from a broad international community, a number of analytic tools have been developed for KF, including a suite of embedded applets (e.g., Contributions, Social Networks, Semantic Overlap, Vocabulary Growth, and Lexical Analysis; see [Teplovs et al., 2007](http://dl.acm.org/citation.cfm?id=1599732)), a standalone Analytic Toolkit (ATK, Burtis, 1998), and more recently, a few independent analytic tools such as [Idea Thread Mapper](http://tccl.rit.albany.edu/wpsite/?page_id=265) and [Knowledge Building Discourse Explorer](http://kbdex.org/). Underlying these development projects is a fundamental emphasis of [knowledge building](http://ikit.org/kbi/knowledge-building)---the theory and pedagogy behind Knowledge Forum---on "embedded, concurrent, transformative assessment" for continual idea improvement. Thus, both the spirits and practice of learning analytics are present within the established line of knowledge building research.

Despite such a strong presence of learning analytics, I have a few complains about the way those analytic tools have been developed. First, developing an embedded analytic applet for the old KF is not a trivial task. Because an applet (written in Java Swing) uses the same communication mechanism as the core KF client, writing it requires a certain level of familiarity with the core KF codebase. This situation makes prototyping new tools especially difficult. Second, the condition for developing those independent analytic tools such as Idea Thread Mapper is not ideal either. Such work requires similar familiarity with KF development stack, and thus demands direct support from the core engineering team. Moreover, because teams in our distributed international community tend to favor a variety of different development stacks (relation vs. non-relation databases, for instance), plenty of redundant efforts have been made to retrieve KF data. We definitely need a more agile and standard way to make KF data accessible.

So when developing the next-generation Knowledge Forum, I have been advocating for **an open Knowledge Forum API**. Thanks to our engineer team's hard work, such an API is finally taking shape. It is currently being used to develop an iPad version of KF. Because of my interests in learning analytics, I am especially interested in building a new technological framework for KF analytics. In this post, I am going to demo the API in [R](http://www.r-project.org/), a statistical programming language widely used by data scientists, to demonstrate how analytics could be compiled using the new API.

*Note: The API is in its preliminary stage. So any suggestion will be appreciated.*

## Setup

I've written [an R wrapper for the KF API](https://github.com/meefen/KF-R) to make it easier to work with the API in R. This library currently depends on two R packages: `RCurl`---to make HTTP calls to the API, and `jsonlite`---to parse JSON objects returned by the API.

After loading the API library functions, you would need to create a 'curl handle' that will be shared by all API calls.

{% highlight r %}
source("kf-api-lib.R") # load the function library

## Create a curl handle that will be shared among API calls
curl = CreateCurlHandle()
{% endhighlight %}

## User authentication

After the server and login information is configured, user authentication can be done with one line of code. The results of authentication contain information about which sections (or knowledge-building communities) I'm currently registered in.

{% highlight r %}
## Login info
host = "http://kf.utoronto.ca:8080/kforum/"
username = "bodong" # YOUR_USERNAME
password = "******" # YOUR_PASSWORD

regs = Authenticate(host, username, password, curl)
regs[, c("sectionId", "sectionTitle")] # check sections I'm in
{% endhighlight %}

```
##                              sectionId              sectionTitle
## 1 416658e6-b49f-4189-8f9a-fe78d8b5f4c1            KF Stress Test
## 2 b1f6fed2-a64e-4bd2-ab8b-393fb2ed1f06 Knowledge Society Network
```

## Retrieve my posts in a community

After being authenticated, I can now access data in communities I'm a member of. Let's first take a look at how posts (or notes) can be retrieved.

With the library, I could get all posts in a specific community and only keep mine.

{% highlight r %}
## Choose a section/community I'm interested in
userId = regs$authorInfo.guid[2]
sectionId = regs$sectionId[2]

## 2. My posts
posts = GetSectionPosts(host, sectionId, curl)
myPosts = FilterPostsByAuthors(posts, userId) # all my posts here
{% endhighlight %}

Then we can do all kinds of things with the results. For example, we can compare the number of my posts with the community average.

{% highlight r %}
authors = do.call("rbind", posts$authors) # all unique authors
tmp = data.frame(author=factor(c("Me","Average"), levels=c("Me","Average")), notes=c(nrow(myPosts), nrow(posts)/length(unique(authors$guid))))
library(ggplot2)
library(ggthemes)
ggplot(data=tmp, aes(x=author, y=notes, fill=author)) +
  geom_bar(colour="black", stat="identity") +
  ggtitle("Number of my posts compared to community average") +
  guides(fill=FALSE) +
  theme_solarized()
{% endhighlight %}

![](/assets/kf-api-compare-with-average.png)

We could also create a calendar to visualize my posting activities.

{% highlight r %}
dates = strptime(myPosts$created, "%b %d, %Y %I:%M:%S %p")
dates_str = as.character(format(dates, format="%Y-%m-%d"))
tmp = data.frame(table(dates_str))
names(tmp) = c("date", "value")
CalendarHeatmap(tmp, title="Posting Activities")
{% endhighlight %}

![](/assets/kf-api-posting-calendar.png)

Obviously I have been not super active in this community.

We can also find out the top terms in my posts.

{% highlight r %}
library(tm)
myNotes = Corpus(VectorSource(myPosts$body))
myDtm <- DocumentTermMatrix(myNotes, control = list(
  stopwords = TRUE, minWordLength = 3,
  removeNumbers = TRUE, removePunctuation = TRUE))
myFreqTerms = findFreqTerms(myDtm, 8, 100)
myFreq = colSums(inspect(myDtm[, myFreqTerms]))
tmp = sort(freq, decreasing=TRUE)
data.frame(term=names(tmp), freq=tmp, row.names=NULL)
{% endhighlight %}

```
        term freq
1  knowledge   24
2   building   21
3       will   17
4  analytics   14
5       note   14
6       view   13
7     badges   11
8       open   10
9     design    8
10      need    8
```

As you can tell, I posted mostly about *knowledge building*, *analytics*, *open badges*, and *design*.

## Inspect a specific view

In Knowledge Forum, a *view* is a 2D space where *notes* (or posts) are organized. It is one of the most important feature that distinguishes KF from threaded discussion tools.

With the API, I could retrieve all views in the current community:

```r
views = GetSectionViews(host, sectionId, curl)
```

Then, I can further inspect one specific view.

```r
viewId = views[15, "guid"] # I'm interested in view #15
view = GetView(host, viewId, curl)
```

With more detailed information about this view, we can count number of its posts and calculate the percentage of *build-ons* among those posts.

```r
nrow(view$viewPostRefs)
nrow(view$buildOns) / nrow(view$viewPostRefs)
```

We could also re-visualize the view, given the location of each note is also stored in the JSON object returned by the API.

```r
ggplot(view$viewPostRefs, aes(x=location$point$x, y=location$point$y)) +
  geom_text(aes(label=postInfo$title), hjust=0) +
  ggtitle(view$title) +
  scale_y_reverse() + theme_bw() +
  theme(axis.title=element_blank(),
        axis.text=element_blank(),
        axis.ticks=element_blank(),
        panel.grid=element_blank())
```

![](/assets/kf-api-revisualize-view.png)

Similar to what's done for my personal notes, we can also find top terms used by posts within this view.

```r
notes = Corpus(VectorSource(view$viewPostRefs$postInfo$body))
dtm <- DocumentTermMatrix(notes, control = list(
  stopwords = TRUE, minWordLength = 3,
  removeNumbers = TRUE, removePunctuation = TRUE))
freqTerms = findFreqTerms(dtm, 8, 100)
freq = colSums(inspect(dtm[, freqTerms]))

tmp = sort(freq, decreasing=TRUE)
data.frame(term=names(tmp), freq=tmp, row.names=NULL)
```

```
        term freq
1       note   45
2       view   33
3      notes   22
4        can   17
5        new   13
6       will   13
7        tap   12
8       work   12
9        add   10
10    chrome   10
11    issues   10
12   version   10
13     ideas    9
14       one    9
15     views    9
16  attached    8
17     build    8
18    design    8
19      idea    8
20       ios    8
21      need    8
22 scaffolds    8
23      text    8
24     title    8
25       use    8
```

And then, I can further find out the overlap between the community's and my own top terms.

```r
intersect(myFreqTerms, freqTerms)
```

```
## [1] "design" "need"   "note"   "view"   "will"
```

## Future work

As a researcher interested in learning analytic tools, I am personally very excited about this API. As shown in this demo, it makes prototyping in R extremely easy. Using `rApache` or `Shiny`, we could further turn prototypes into analytic tools that can be seamlessly integrated within the new KF. Of course, you could choose to access the API in other languages such as Python and Java as well.

However, the API is still in its preliminary stage. More work needs to be done to make user clicklog accessible. Meanwhile, it should also support posting data backwards to KF.

In this year's [Knowledge Building Summer Institute](http://ikit.org/summerinstitute2014/) in Quebec City, I will be leading a knowledge building analytics workshop to further discuss the design of this API. Other broader issues related to epistemological, ethical, and technological aspects of knowledge building analytics will also be explored. Stay tuned.
