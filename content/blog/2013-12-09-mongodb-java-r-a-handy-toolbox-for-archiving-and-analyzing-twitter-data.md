---
date: '2013-12-09'
title: MongoDB + Java + R = A handy toolbox for archiving and analyzing Twitter data
categories:
- blog
tags:
- social media
- mongodb
- r
- twitter
---

I've been using [Martin Hawksey](https://twitter.com/mhawksey)'s
brilliant [Google Spreadsheet
TAGS](http://mashe.hawksey.info/2013/02/twitter-archive-tagsv5/) for
archiving Twitter data
for [y](http://bodongchen.com/blog/2012/04/overview-of-aera2012-tweets/)-[e](http://bodongchen.com/blog/2012/10/225/)-[a](http://bodongchen.com/blog/2013/02/demo-of-using-twitter-hashtag-analytics-package-to-analyze-tweets-from-lak13/)-[r](http://bodongchen.com/blog/2013/12/top-links-from-the-mooc-research-conference-twitter-backchannel-mri13/)-s.
It works very well, and allowed me to develop little R toys
like [twitterytics-shiny](https://github.com/dirkchen/twitterytics-shiny) to
interactively explore Twitter archives.

However, I have a few complains. First, Twitter API authentication needs
to be set up for each archive. The task which require a few steps in
Google Spreadsheet is not trivial. Second, I often ended up getting
hundreds or even thousands of duplicates that may cause the file size to
exceed Google Spreadsheet's size limit. Third, sometimes the getTweets()
function powered by Google Code (I think) fails for unknown reasons.
Although I still greatly enjoy TAGS, for these reasons I have been
wishing to have an easier and more liable way to archive theoretically
unlimited number of tweets for quite a while. So when I read a post
about *archiving tweets with
MongoDB* ([part1](http://thinktostart.wordpress.com/2013/10/22/build-your-own-twitter-archive-and-analyzing-infrastructure-with-mongodb-java-and-r-part-1/)
&
[part2](http://thinktostart.wordpress.com/2013/12/09/build-your-own-twitter-archive-and-analyzing-infrastructure-with-mongodb-java-and-r-part-2/comment-page-1/#comment-448))
by [Julian Hillebrand](https://twitter.com/julianhi) today, I couldn't
stop myself from trying it out.

[![mongoDB-logo](http://bodongchen.com/blog/wp-content/uploads/2013/12/mongoDB-logo-1024x341.png)](http://bodongchen.com/blog/wp-content/uploads/2013/12/mongoDB-logo.png)

Julian's [code](https://github.com/JulianHill/TwitterArchive) works! But
after a bit playing and tweaking, I think the solution I ended up using
became quite distinctive and deserved an independent post. So below is
what I did, which I think contains some improvement over the original
solution.

1. Setup MongoDB
----------------

You can download MongoDB [here](http://www.mongodb.org/downloads) and
install it on your computer as Julian suggested. Or, you can using
MongoDB hosting services in the cloud, like
[MongoLab](https://mongolab.com/). I used the free subscription on
MongoLab. It was very easy to setup (believe me, this was my first time
partying with MongoDB), and you don't need to install any other things
(like the Netbeans MongoDB plugin).  Plus, you might want to keep it
running when your laptop is off so it's better to use something in the
cloud. So I strongly recommend MongoLab. If you choose to follow this
path, there're around 3 steps:

-   **Register** for a MongoLab free subscription
-   **Create a new database**, say "twitter-mongo"
-   Click into the database and **add a database user**; record the
    username/password for later use

It will definitely help to read MongoDB's
[manual](http://docs.mongodb.org/manual/tutorial/getting-started-with-the-mongo-shell/),
but I really got as far as the first page.

2. Setup Java project and run the code
--------------------------------------

Java code is used to retrieve tweets through Twitter API and save them
into MongoDB. Julian explained how his code works in details. I did some
tweaks to make the settings more visible and easier to modify. My code
is posted in this
[gist](https://gist.github.com/dirkchen/7885000). Download
TwitterLoop.java and do the following few things:

-   **Create a Java project** in your favorite Java IDE (e.g., Netbeans)
    and put the Java file in
-   **Add dependencies**:
    [twitter4j](http://twitter4j.org/en/index.html#download) (core) and
    [mongodb-java-driver](https://github.com/mongodb/mongo-java-driver/downloads)
-   In the Java file, **change settings** for MongoDB and Twitter API

Then you should be able to directly run the Java file and start
collecting tweets. Each time when you run the file, you will need to
type in the search keyword (e.g. "\#mri13") for Twitter. Then the file
will repeatedly retrieve 100 tweets containing that keyword from Twitter
every 60 seconds (these two numbers can also be customized in the Java
file), and put new ones into MongoDB. Theoretically you can have Java
instances running forever. (As Julian mentioned, there should be a
better way to do this loop, for eaxmple using streaming API.)

If you run the Java file twice for two different Twitter archives, say
"\#mri13" and "\#edtechchat", two MongoDB *collections* will be created
respectively with these two names.

3. Retrieve tweets in R from MongoDB for analysis
-------------------------------------------------

After tweets are collected in MongoDB, querying data in R becomes very
straightforward.

{% highlight r %}
library(rmongodb)

## Host info and credentials
host <- "ds053858.mongolab.com:53858"
username <- "your_username"
password <- "your_pass"
db <- "twitter-mongo"

## Connect to mongodb
mongo <- mongo.create(host=host, db=db,
                      username=username, password=password)
{% endhighlight %}

Check how many collections are in the database:

{% highlight r %}
## Get a list of collections within our namespace
#  here I used each collection for a twitter archive
mongo.get.database.collections(mongo, db)
{% endhighlight %}

Do some simple queries in the \#mri13 collection:

{% highlight r %}
## Create a string that points to the namespace
#  the collection I'm interested in is "#mri13"
collection <- "#mri13"
namespace <- paste(db, collection, sep=".")

## Check the total number of tweets in "#mri13"
mongo.count(mongo, namespace, mongo.bson.empty())
{% endhighlight %}

Build a query to find how many tweets were posted by me

{% highlight r %}
buf <- mongo.bson.buffer.create()
mongo.bson.buffer.append(buf, "user_name", "bodongchen")
query <- mongo.bson.from.buffer(buf)
# get the count
count <- mongo.count(mongo, namespace, query)
count
 
## Get all tweets posted by me
tweets <- list()
cursor <- mongo.find(mongo, namespace, query)
while (mongo.cursor.next(cursor)) {
  val <- mongo.cursor.value(cursor)
  tweets[[length(tweets)+1]] <- mongo.bson.value(val, "tweet_text")
}
length(tweets)
{% endhighlight %}

Retrieve all tweets in this collection/archive as a dataframe:

{% highlight r %}
## Retrieve all tweets and put into a dataframe
library(plyr)
df_arch1 = data.frame(stringsAsFactors = FALSE)
cursor <- mongo.find(mongo, namespace)
while (mongo.cursor.next(cursor)) {
  # iterate and grab the next record
  tmp = mongo.bson.to.list(mongo.cursor.value(cursor))
  # make it a dataframe
  tmp.df = as.data.frame(t(unlist(tmp)), stringsAsFactors = F)
  # bind to the master dataframe
  df_arch1 = rbind.fill(df_arch1, tmp.df)
}
dim(df_arch1)
{% endhighlight %}

Start playing with another collection/archive named "\#edtechchat":

{% highlight r %}
### Try with another collection
collection2 <- "#edtechchat"
namespace2 <- paste(db, collection2, sep=".")
mongo.count(mongo, namespace2, mongo.bson.empty())
{% endhighlight %}

The R code above is also included in the
[gist](https://gist.github.com/dirkchen/7885000).

Conclusions
-----------

This solution brought together by MongoDB, Java, and R seems to me a
proof-of-concept of a reliable and scalable way to automatically archive
and analyze tweets. Here, Java can be easily replaced by Python or R. It
might evolve into a nice toolbox for hacking Twitter data. I believe
there will be a lot of fun.
