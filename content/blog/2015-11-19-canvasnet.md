---
date: '2015-11-19'
title: "CanvasNet: Formative feedback for 'social learning' on Canvas"
categories: blog
tags:
- learning analytics
- social network analysis
- formative assessment
- R
comments: true
---

I have been teaching an undergraduate course using [Canvas](https://canvas.instructure.com/) this semester. I don't remember how it happened because I'm essentially a disbeliever in Learning Management Systems (LMS). I believe one's learning should not be *managed*. "LMS is the minivan of Education," [says Phil Hill](http://mfeldstein.com/lms-is-the-minivan-of-education-and-other-thoughts-from-lili15/). Even better, "the LMS is more like a bus than a minivan - someone else is driving, it only travels on a pre-arranged route, the bus is often late but you still have to be on time because it won't wait if you miss it" -- [says Stephen Downes](http://www.downes.ca/post/63849). However, to show my mistrust in the 'minivan' or 'bus', I didn't choose to avoid it but to jump on board and *play* with it.

<blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr">&#39;The LMS is the minivan of education—everyone has one and no one is proud of it&#39; - <a href="https://twitter.com/PhilOnEdTech">@PhilOnEdTech</a> <a href="https://twitter.com/hashtag/opened15?src=hash">#opened15</a> <a href="https://t.co/gdel0oj8Pn">pic.twitter.com/gdel0oj8Pn</a></p>&mdash; Tom Evans (@taevans) <a href="https://twitter.com/taevans/status/667028440046899200">November 18, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

As a social construtivist researcher, social interaction is a must in my teaching. Because the course I am teaching is writing-intensive, posting some text each week in the forum is an important part of course participation. As a novice (online) instructor, I've been trying to find means to nurture social interaction in the forum. (Btw, regardless of 'bells and whistles' of features for *management*, the discussion forum on Canvas is unsurprisingly dully designed.) As an R tinkerer, I thought it might be neat to write some tools to provide formative feedback to my students on their social and conceptual engagement.

- *Social engagement*. To help students reflect on their social engagement, social network analysis (SNA) becomes a natural choice. However, it is not always clear based on the literature which kinds of information from SNA could be helpful for students. A socigram? Network metrices? Or written interpretation of them?
- *Conceptual engagement*. One challenge I see in my class is to bring students to become aware of each other's contributions. Different students -- bringing with them different interests and experiences -- were discussing different things. A challenge is to present a high-level conceptual landscape of discussion hoping students could become aware of and eventually take-up things they would otherwise neglect.

## CanvasNet

With these goals in mind, I put together a rough plan and designed an analytics-driven "intervention" for my class. The analytics is simple -- social network analytics and a wordcloud based on weekly discussions. Pedagogical design included written interpretations and encouragements that went into weekly announcements on Canvas.

In researching means to develop the feedback tools, I stumbled upon Martin Hawksey's [blog post](https://mashe.hawksey.info/2013/02/lak13-recipes-in-capturing-and-analyzing-data-using-sna-on-canvas-discussions-with-nodexl-for-when-its-not-a-snapp/) on getting Canvas discussion forum into Google Spreadsheet and then exporting data for social network analysis using NodeXL. Following Martin's recipe, it took 20 minutes to get things setup before Google Spreadsheet started to take care of data gathering and storage for me.

With Google taking care of data, I wrote a Shiny app in R which reads data from Google, processes social interactions and posts (using the `igraph` and `tm` packages respectively), and returns two simple interactive visualizations to students.

- **A sociogram**. A visualization of interaction network among students. The teacher is hidden by default, mainly because the design of Canvas (and LMS in general) implicitly suggests all discussions originate from the teacher. Students could identify themselves and explore who they are talking with by interacting with the sociogram. Some simple social network metrics, e.g., degrees and density, are provided.

![example figures here](/assets/canvasnet-sociogram.png)

- **A wordcloud**. A wordcould visualizing most frequent words used in discussion (in the past two weeks by default). Further feedback is provided that highlights frequent terms the current student has and has *not* engaged with so far. In addition, the number of words to display and the frequency threshold could be adjusted. One could also click on a word to find out its frequency.

![example figures here](/assets/canvasnet-wordcloud.png)

Data collection is ongoing. Student beliefs in 'social learning' have been collected through a questionnaire. Online focus groups were conducted to explore students' experience of social interactions in this course. We will interview some students to understand the usefulness of this tool.

My intuition is the current version of this tool will NOT work for a variety of reasons. The lack of dialogues around this tool is one possible factor. The habit of learning as individuals is another contributor. Lessons learned will be used to inform the next design cycle.

## Calling the Canvas API from R

Supposing we need to remove the dependency on Google Spreadsheets, calling the Canvas API directly from R is also quite straightforward. Below is a (sort of) minimal example to play with:

```r
library(RCurl)
library(jsonlite)
library(dplyr)

#################################
## Functions
#################################

CreateCurlHandle <- function() {
  ### Create a curl handle that will be shared among API calls

  library(RCurl)
  curl = getCurlHandle()
  curlSetOpt(cookiejar = "",
             followlocation = TRUE,
             curl = curl) # do not need to read the cookies
  return(curl)
}

CleanJSONText = function(text) {
  ## Clean json text that might cause lexical error when parsing

  text = gsub("\n", " ", text)
  text = gsub("\t", " ", text)
  text = gsub("\\\\<", "<", text)
  text = gsub("<img.*?>", "", text) # get rid of images
  text = gsub("\r", " ", text)
  return(text)
}

#################################

## Baseurl and access token
baseUrl = "https://YOUR_HOST.instructure.com/api/v1/courses"
token = "YOUR_CANVAS_TOKEN"

curl = CreateCurlHandle()

## Authenticate
auth = tbl_df(fromJSON(
  getForm(baseUrl, access_token = token, curl=curl),
  flatten = TRUE
))
glimpse(auth)

## Pick a course
courseUrl = paste0(baseUrl, "/", YOUR_COURSE_NUMBER)

## Retrieve all topics
topicsUrl = paste0(courseUrl, "/discussion_topics")
json = getForm(topicsUrl,
               .opts = list(httpheader = c(Authorization=paste("Bearer", token))),
               # access_token = token,
               curl=curl)
topics = tbl_df(fromJSON(CleanJSONText(json), flatten = TRUE))
data.frame(topics %>% select(id, title, url))

## Pick one topic, and get the full topic
topicUrl = paste0(topicsUrl, "/", topics$id[4], "/view")
json = getForm(topicUrl,
               access_token = token,
               curl=curl)
topic = fromJSON(CleanJSONText(json), flatten = TRUE)
participants = topic$participants
posts = topic$view
replies = do.call("rbind", posts$replies)
# from replies social network could then be analyzed ...
```

## Wrap up

This post mainly reports on a technological effort to develop a simple feedback tool for online discussion on Canvas. The current design is to harness Canvas data using Google Spreadsheet and then visualize data using an R Shiny app. Reading data directly from Canvas could be an option in future design and development. The efficacy of the simple prototype remain unclear and likely to be challenged. Tons of issues need to be further explored.
