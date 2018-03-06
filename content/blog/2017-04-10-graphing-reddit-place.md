---
date: '2017-04-10'
title: "Graphing the Reddit Place Sensation with Neo4j"
categories: blog
tags:
- graph database
- social media
- neo4j
comments: true
image: /assets/article_images/ajWiAYi.png
---

I'ver never liked the April Fool's Day, until this year when [Reddit](https://www.reddit.com/) decided to [launch a social experiment](https://www.reddit.com/r/announcements/comments/62mesr/place/) called [Reddit Place](https://www.reddit.com/r/place/).

The idea is simple. The whole world -- or all Reddit users -- were given a 999 x 999 blank canvas to draw on. Some simple rules apply:

> Each user could choose one pixel from 16 colors to place anywhere on the canvas. They could place as many pixels of as many colors as they wanted, but they had to wait a few minutes between placing each one. ([source](http://sudoscript.com/reddit-place/))

During the following 72 hours, amazingly interesting things happened on this 999 x 999 canvas. Below is a gif that gives you a glimpse into what had happened. Numerous accounts of this event have been posted. See [this post](http://sudoscript.com/reddit-place/) for a good overview, and more posts can be found at the [Reddit Place](https://www.reddit.com/r/place) itself.

![](https://i.redd.it/5p68ukzkwdpy.gif)

## Graphing the Reddit Place with Neo4j

The Reddit Place as a web-based social phenomenon will be remembered and studied by many people. I didn't follow this event at all but was amazed by the various types of participating users, sub-communities who self-organized to achieve certain goals, clashes and fights, evolving rules, impressive artworks, and so on -- all that happened on this little canvas. I'm especially intrigued by the emergent, self-organizing processes of constructing, destructing, negotiating, and re-constructing among numerous users and user networks supported by all kinds of communication tools (mostly Reddit itself).

With [a data dump](https://www.reddit.com/r/PlaceDevs/comments/637ynq/a_datadump_but_from_a_different_scraper/) that captured the history of this event, I could not resist myself from playing with it using [Neo4j](https://neo4j.com/).

### Importing data

To begin with, I wrote the following Cypher scripts to import the csv dump into Neo4j:

{% highlight cypher %}
// Set constraints
CREATE CONSTRAINT ON (p:Point) ASSERT p.location IS UNIQUE;
CREATE INDEX ON :User(name);

// Insert data
USING PERIODIC COMMIT 1000
LOAD CSV FROM "file:///export.csv" AS l
WITH l, [toInt(l[1]), toInt(l[2])] AS loc
WHERE l[3] IS NOT NULL
MERGE (p:Point {location: loc})
  ON CREATE SET p.location = loc, p.count = 1
  ON MATCH SET p.count = p.count + 1
MERGE (u:User {name: l[3]})
  ON CREATE SET u.name = l[3], u.count = 1
  ON MATCH SET u.count = u.count + 1
MERGE (u)-[r:PAINT]->(p)
  ON CREATE SET r.count = 1, r.ids = [toInt(l[0])],
    r.colors = [toInt(l[4])], r.times = [toInt(l[5])]
  ON MATCH SET r.count = r.count + 1,
    r.ids = r.ids + toInt(l[0]),
    r.colors = r.colors + toInt(l[4]),
    r.times = r.times + toInt(l[5]);
{% endhighlight %}

The figure below demonstrates the *graph model* of the created Neo4j graph database. The model is quite simple and intuitive, including two node types named `User` and `Point` and one relationship type named `Paint`.

![](/assets/article_images/r-place-graph-model.png)

It took my computer ~22 minutes to create 1.6 million labels, 1.6 million nodes, 28.8 million properties, and 4.13 million relationships in this graph database, the size of which ended up to be 4.30 GB.

### General queries

After data were loaded, I did some quick queries.

**First, who were the most active users?** User `itsnotlupus` won the game as s/he painted for 177 times. This may not sound much but if you multiple 177 by 5 minutes (the 'cooldown' time), you will find the user spent roughly 15 hours painting or contemplating the next pixel on the canvas. This time amount does not include activities in other communication tools.

**Where did `itsnotlupus` paint?** Below is a graph showing this user (in the center) and 100 pixels s/he painted on. Note that each pixel is identified by its coordinates in the 2D canvas.

![](/assets/article_images/top-user.png)

I noticed this user painted a whole lot near `Point [380, 880]`. By clicking on the [380, 881] Point node, see below, I could check who else have painted on that spot. 16 other users have painted there. Maybe there were some interesting collisions on that single pixel?

![](/assets/article_images/top-user-clashes.png)

**Which colors did `itsnotlupus` use?** It appeared `itsnotlupus` painted <span style="background-color:#e59500">#E59500</span> for 104 times, and <span style="background-color:#e50000">#E50000</span> for 70 times. Do those two colors belong to specific clans `itsnotlupus` was affiliated with?

{% highlight cypher %}
MATCH (u:User {name: "itsnotlupus"})-[r:PAINT]->()
WITH collect(r.colors) as colors
UNWIND colors as array
UNWIND array as color
RETURN color, count(color) as count
ORDER BY count DESC LIMIT 10
{% endhighlight %}

### The Blue Corner

Based on [this post](http://sudoscript.com/reddit-place/), the lower-right corner was occupied by [Blue](https://www.reddit.com/r/BlueCorner/). So I checked the corner pixel [999, 999]. The following Cypher query returned a total of **`10,121` user actions on that single pixel**. The figure that follows shows 100 of those users who painted at [999, 999].

{% highlight cypher %}
MATCH (p:Point {location: [999, 999]})<-[r:PAINT]-()
RETURN count(r)
{% endhighlight %}

![](/assets/article_images/999x999-users.png)

**Top painters in that corner** are listed in the figure below. Querying the top [999, 999] painter `MrMeltJr` I found him painting <span style="text-shadow: 4px 4px 2px #0000EA">`blue (#0000EA)`</span> predominantly (105 out of 116 times). He was clearly a member of the Blue Corner sub-community.

![](/assets/article_images/999x999-top-users.png)

**What was the most used color in that corner?** The following query found the most dominant color to be <span style="text-shadow: 4px 4px 2px #0000EA">`#0000EA`</span>, which appeared for 7400 times, followed by <span style="text-shadow: 4px 4px 2px #820080">`#820080`</span>'s 2055 times. This finding could be confirmed by the gif above.

{% highlight cypher %}
MATCH (p:Point {location: [999, 999]})<-[r:PAINT]-()
WITH collect(r.colors) as allColors
UNWIND allColors as array
UNWIND array as color
RETURN color, count(color) as count ORDER BY count DESC LIMIT 10
{% endhighlight %}

## More Fun to Come

These queries are far from even scratching the surface of the complex social phenomenon. Two aspects I'm especially interested in exploring (if I have time) are the `temporal` aspect of user actions on single pixels and the `spacial` aspect of changes with neighboring pixels. In addition, it would also be useful if we could connect communication and coordination among users and communities external to the canvas.

Yes, now I see the April Fool's Day could be fun!
