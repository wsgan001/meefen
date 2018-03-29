---
title: "Considering Time in Education"
categories: blog
tags: [temporality, learning analytics]
---

date: '2018-03-08'

It was 2016-08-07 when [the call for papers of our *Special Section on Temporal Analyses of Learning Data*](http://learning-analytics.info/journals/index.php/JLA/announcement/view/119) was posted on the *Journal of Learning analytics* (JLA) website. It was even earlier, probably around late 2014, when Alyssa Wise, Simon Knight, Britte Cheng and I teamed up for the temporality workshop series at the *Learning Analytics and Knowledge (LAK)* conference. At that time, I was still in Toronto, Alyssa in Vancouver, Simon in the UK, and Britte at SRI. This April, 3.5 years after conceiving the temporality workshop series, the second part of the *Special Section on Temporal Analyses* will finally come out in JLA.

As you could read in [our editorial](#), we're trying to draw the community's attention to a number of critical questions for temporal analysis (by researchers) and temporal analytics (that move from research towards practice). One brief yet vital section of this editorial reflects on the influence of "measured time" on "experienced time" in education. We did not have enough luxuary (both in terms of space and time) to go as deep as we wished in the editorial. In this blog post, I hope to expand on this important discussion from ontological, epistemological, and analytical standpoints.

## Our understanding of time is never settled

*Time* is discussed, and quite often disputed, in philosophical texts. Deep reflection on time dates back to thousands of years in both Western and Eastern philosophies. Many key questions remain debated nowadays. For example: Is time real? Does time have a beginning or an end? Does time progress linearly? Are there parallel timelines? Which can be considered 'primitive'---instant *time points* or *time durations*? How are time and space related? What exactly is time and how can humans make sense of it? Human understanding of time, reflected in texts of all kinds, is very much unsettled ontologically, epistemologically, and psychologically (Pöppel 2004).

Narrowing down to the debate on *time points* and *time durations* for instance, ...

As of human perception of time, great complexity has been uncovered in cognitive, sensory, physical, biophysical, and neural aspects [@Poppel2004-ge]. For example, a time period shorter than 40 miliseconds is perceived as a 'time point', whereas one's subjective present lasts for approximately 2 to 3 seconds.

## Our relation to time is often implictly assumed

At the individual level, how we conceive and relate ourselves to time is of huge importance, which is rarely explicitly discussed. Is one's time a resource? If so, how is it allocated? How is one's actions coordinated in relation to time? How to time an action to achieve a goal? How to time an action in relation to other actions to achieve a goal? How to time an action in relation to other actions by other agents to achieve a goal? Or do we simply think time as time, nothing more and nothing less? We rarely engage with these types of questions individually. Our relation with time is usually maintained at the *first-order* at best; that is, we think about or plan our use of time or the timing of personal actions in a social context. Yet we rarely reflect on the *second-order* relation with time---XXX

At the society level, looking back into the human history, it is apparent that as societies evolve, our relation with time has gone through dramatic changes. Our lived experiences are fundamentally shaped by our conception of time (and space). In ancient times a hallmark of an advanced civilization is the precision of its calendar because it would inform crucial societal activities such as farming and hunting. Farmers consult calendars to decide when to plant seeds, while hunters would adjust their group activities based on animal birth rates, migration, and so forth. They understand and internalize rhythms of the nature and also construct ones in order to coordinate complex social activities. As the "clock time" or mechanical time became established as a standard and spread around the globe, our relation with time became increasingly finely defined. The time zone system was nonexistent before the steam engines, and now it is amazing how a group of people from several corners of the globe would show up in a virtual meeting right on time, with a timed agenda, and would wrap up the meeting right on time in order to move on to the next activity on each one's calendar. Time slots on our personal calendars are connected (e.g., via a calendar invite) and the ways in which we could coordinate our time at various levels are more sophisticated than ever.  The societies and cultures we grow out of and live in greatly shaped our relations with time, which in turn shape how our societies operate. Thus, for any deep temporal analysis of human activities we need to reflect upon these relations.

More recently, globalization has resulted in a compression of time (and space) (Edwards & Usher, 200X).

> Central to globalisation is...  (p. 27)

This speaks to, for instance, the context of MOOC and the notion of international classrooms (edX report) that have indeed blabla.

However, temporal analytics are necessarily making claims based on a dominant view of time and order (one that either represents Western institutions or is embedded in the MOOC design) and sometimes gets quite arrogant against views and realities held by the learners. For MOOCs, more research is needed to understand learnes from non-dominant cultures and background are experiencing ..,

Education in particular has strict temporal boundaries that would dictate daily educational practice. Yet they are also usually implicitly assumed, just like our general relations to time at the individual and societal level.  Since the industrial age, we started to place learners into grade schools based on their age. Like other institutions, we slice up a calendar year into semesters or quarters, and divide a day into sessions for varied educational activities. In one class session, detailed planning is often championed and a “model” teacher may crush a session into minutes to demonstrate one’s dedication to education. In computer-supported learning environments, we implement sophisticated mechanisms to record timestamped learner activities; we build dashboards to present temporal graphs related to one’s progress in a domain. It seems in education we are also moving towards finer planning, monitoring, and controlling over our relation with time. Learning analytics as a field offers rich, exciting opportunities in this area.

## Time and learning

Such an emphasis on controlling and aligning phenomena with time is unsurprising. Learning is fundamentally about change, which takes time. (Philosophers would also agree change is essential to time as well [McTaggart; entropy theory].) Learning theories have explicit and implicit assumptions and considerations of how changes take place over time. In other words, learning theories are grounded in assumed theories of time. For example, Piaget’s theory of stages of cognitive development, and his thoughts on genetic epistemology in particular, is fundamentally about tracing the origins and trajectory of human knowledge across one’s lifespan [REF]. On a relatively shorter timescale, self-regulated learning is inherently concerned with temporal sequences and patterns (Winne 2014). Broadening from a single person to consider greater complexity related to groups, “interaction trajectory” in CSCL is concerned with how interaction among students lead to the development of understanding over time (Furberg and Ludvigsen 2008). Expanding further to larger social structures, communities, and cultures, Activity Theory deals with historical development of activity systems that involve multiple parties [REF]. These theories of learning would inform analytical choices of temporal analysis---choices such as whether to focus on timepoints or durations, changes over time or temporal organizations, timescales, reference points and frames in temporal analysis, and the relationship between temporal analysis and other analytical angles.
-	Given time constraints placed by education regimes, the concern is to incur satisfactory “positive” changes in learners within a certain period of time. [How about no-change? Is it okay to stay unchanged?]

## Time and technological environments

Given temporal analyses in the learning analytics community are often situated in computer-based environments, it is also key to recognize assumed theory of time built with/into computer systems, as well as what data they capture and how they are captured. From temporal reasoning perspectives, artificial intelligence (AI) scholars such as (Knight and Ma 1993) have worked on various ways of representing time in temporal systems, to aid for reasoning in AI. In the learning analytics community, and the broader ecosystem it operates within (which includes important information system standards such as xAPI), we often take as granted that learning actions are timestamped in computer systems and those timestamps are temporal information we can draw upon. However, we need to be aware of a myriad of inferences we make from those timestamps (which, philosophically speaking, treats time points instead of durations as being primitive) to our claims of learning phenomena. Take MOOC learning for example, we often assume within a single login session, the amount of time (duration) a learner spends on a specific course page is determined by two adjacent timestamps. [another/better example?] While we can reasonably argue this measure is accurate enough, we should also be aware temporal considerations built into computer systems and their data would either hamper or empower temporal analysis.

## Time and Artificial intelligence

Finally, existing temporal analysis techniques were built with specific analytical goals related to temporality. @Reimann2009-pm distinguishes two important categories: time---as related to questions such as when an event take place, how long it lasts, and how a state change over time; and order---focused on temporal organization of events. A variety of temporal analysis techniques, as we see in this Special Section, are designed with an emphasis on one over the other. Sometimes it could beneficial to experiment with multiple techniques for converging or complementary findings (Chen et al. 2017). In some other cases, like studies included in the Special Section, we should take the liberty to propose new temporal measures and techniques. In addition to the time vs. order distinction, we should clearly delineate the boundary between temporality and causation in temporal analysis, as they are too often mixed with each other [REF]. This is particularly important when temporal analysis is applied in practice to make impactful changes. We need to avoid making deterministic and prescriptive claims (in Fatalistic terms) based on temporal observations even though how causation can be drawn from temporal observations remains debated [REF].


## Unite time and space in educational theories

There is an urgent need to reunite time and space in educational considerations. While many educational theories are fundamentally about time (e.g., stages of development), there is increasing recognition of learning happening in different spaces, palces, and socio-cultural-political contexts.  (Edwards & Usher). How could we recognize these -- from learning analytics standpoints...