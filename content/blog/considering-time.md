---
title: "Considering Time in Education"
categories: blog
date: '2018-04-15'
tags: [temporality, learning analytics]
---

![](/images/article_images/25216272279_4278853fc4_z.jpg)
*(Photo Credit: [Luca Florio](https://www.flickr.com/photos/elle_florio/25216272279))*

It was on August 7, 2016 when [the call for papers of our *Special Section on Temporal Analyses of Learning Data*](http://learning-analytics.info/journals/index.php/JLA/announcement/view/119) was posted on the *Journal of Learning analytics* (JLA) website. It was even earlier -- probably around late 2014 -- when Alyssa Wise, Simon Knight, Britte Cheng and I teamed up for the temporality workshop series at the *Learning Analytics and Knowledge (LAK)* conference. At that time, I was still in Toronto, Alyssa in Vancouver, Simon in the UK, and Britte at SRI. This April, 3.5 years after conceiving the temporality workshop series, [the second part of the *Special Section on Temporal Analyses*](http://learning-analytics.info/journals/index.php/JLA/issue/view/427/showToc) has finally come out in JLA.

As you can read in [**our JLA editorial**](http://learning-analytics.info/journals/index.php/JLA/article/view/5940), we try to draw the community's attention to four critical questions for *temporal analysis* (typically by researchers) and *temporal analytics* (that move from research towards practical ends):

![](/images/article_images/critical-questions.jpg)

One brief, yet important, section of this editorial reflects on **the influence of *measured time* on *experienced time* in education**. In the editorial, we did not have the luxury -- in terms of both time and space -- of exploring this issue as deep as we could. In this blog post, I hope to expand on this important issue from multiple angles.

## Our understanding of time is never settled

*Time* is discussed, and quite often disputed, in philosophical texts. Deep reflection on time dates back to thousands of years in different philosophical traditions (e.g., Greek, Indian, Chinese philosophies). Many key questions remain debated nowadays. For example:

- Is time real?
- Does time have a beginning or an end?
- Does time progress linearly?
- Are there parallel timelines?
- Which can be considered 'primitive' -- instant *time points* or *time durations*?
- How are time and space related?
- How do human beings sense time?

This list of questions can keep going. One sure thing is: **Our understanding of time**, reflected in philosophical thinking of all kinds, **is [very much unsettled](https://plato.stanford.edu/entries/time/)** -- ontologically, epistemologically, and psychologically.

<!-- Narrowing down to the debate on *time points* and *time durations* for instance, ... -->

<!-- Take human perception of time, for example, great complexity has been uncovered in cognitive, sensory, physical, biophysical, and neural aspects (Pöppel 2004). For example, a time period shorter than 40 milliseconds is perceived as a 'time point', whereas one's subjective present lasts for approximately 2 to 3 seconds. -->

## Our relation to time is often implicitly assumed

At the individual level, how we conceive and relate ourselves to time is very important but rarely articulated.

- How is *time* related to our perception, memory, decision-making, or action?
<!-- - Is one's *time* a resource? -->
- How are one's actions coordinated in relation to time?
- How to *time* an action to achieve a goal? How to time an action in relation to other actions to achieve a goal? How to time an action in relation to other actions by other agents (people, machine, etc.) to achieve a goal?
<!-- - Or do we simply think time as time, nothing more and nothing less? -->

We rarely engage with these types of questions as individuals. Our relation with time is usually maintained at the *first-order* at best; that is, we think about or plan our use of time or the timing of personal actions within a social context. **Yet we rarely reflect on the *second-order* relation with time; that is how our relation with time -- both perceived and enacted -- is impacting us as individuals and a society.**

At the societal level, looking back into the human history, it is apparent that as societies evolve, our relation with time has gone through dramatic changes. Our lived experiences are fundamentally shaped by our conception of time (and space). In ancient times a hallmark of an advanced civilization is the precision of its calendar because it would inform crucial societal activities such as farming and hunting. Farmers consult calendars to decide when to plant seeds, while hunters would adjust their group activities based on animal birth rates, migration, and so forth. Our ancestors understood and internalized rhythms of the nature and also constructed ones in order to coordinate complex social activities. The societies and cultures we grow up with and live in greatly shaped our relation with time, which in turn shape how our societies operate. Our relation with time gets built in [languages we speak, which in turn shape how we perceive time](https://www.sciencedaily.com/releases/2017/05/170502112607.htm).

As the "clock time" or [mechanical time](http://www.britishmuseum.org/explore/themes/time/mechanical_time.aspx) became established as a standard and spread around the globe, our relation with time became increasingly finely defined. [The time zone system came to exist because of steam engines](https://www.history.com/this-day-in-history/railroads-create-the-first-time-zones), and now it's dictating all sorts of human communication. The reordering of space and time was/is an undercurrent of colonization, modernization, and globalization (Edwards & Usher, 2000). Now time slots on our personal calendars have become inter-connected, and the ways in which we could coordinate our time at various levels are more sophisticated than ever. As a result, any in-depth temporal analysis of human activities requires a deep look at our second-order relation with time.

<!-- More recently, globalization has resulted in a compression of time (and space) (Edwards & Usher, 200X).

> Central to globalisation is...  (p. 27) -->

## Temporal considerations are built into technological environments

Given human activities are increasingly mediated by computer-based environments, it is also key to recognize assumed theories of time built into computer systems, as well as what data they capture and how they are captured in relation to time.

From temporal reasoning perspectives, for instance, artificial intelligence (AI) scholars Knight and Ma (1993) have worked on various ways of representing time in temporal systems decades ago. They explain:

>The most common theoretical basis is the standard time-point system assumed by classical physics. In this theory, the time domain consists of a continuum of time points, isomorphic to  the real line. Time intervals are taken as intervals on the real line, and duration of intervals is the real number difference of their start and end points. However, for many applications, particularly those in artificial intelligence and natural language understanding, the time-point system is not ideal for either the expression of temporal facts, or for the storage and organisation of incomplete temporal knowledge. (p. 401)

In the learning analytics community, and the broader ecosystem it operates within (which includes important information system standards such as xAPI), **we often take *the standard time-point system* for granted**. We accordingly engineer computer systems to tag learning actions by timestamps, which then get used for temporal analysis and reasoning. However, we need to be aware of a myriad of inferences we make from those timestamps to our claims of learning phenomena. Take MOOC learning for example, we often assume within a single login session, the amount of time (duration) a learner spends on a specific course page is determined by two adjacent timestamps. While we can reasonably argue this inferred measure is good enough, **we as a community should be aware of temporal considerations as such built into learning systems and data**, as well as their implications for temporal analyses.

<!-- ## Time and Artificial intelligence

Finally, existing temporal analysis techniques were built with specific analytical goals related to temporality. @Reimann2009-pm distinguishes two important categories: time---as related to questions such as when an event take place, how long it lasts, and how a state change over time; and order---focused on temporal organization of events. A variety of temporal analysis techniques, as we see in this Special Section, are designed with an emphasis on one over the other. Sometimes it could beneficial to experiment with multiple techniques for converging or complementary findings (Chen et al. 2017). In some other cases, like studies included in the Special Section, we should take the liberty to propose new temporal measures and techniques. In addition to the time vs. order distinction, we should clearly delineate the boundary between temporality and causation in temporal analysis, as they are too often mixed with each other [REF]. This is particularly important when temporal analysis is applied in practice to make impactful changes. We need to avoid making deterministic and prescriptive claims (in Fatalistic terms) based on temporal observations even though how causation can be drawn from temporal observations remains debated [REF]. -->

<!-- ## Time, learning, and impact

Learning is fundamentally about change, which takes time. (Of course, philosophers like [John McTaggart](https://plato.stanford.edu/entries/mctaggart/) would also agree change is essential to time as well.) In the JLA editorial, we pointed out that learning theories have explicit and implicit assumptions and considerations of how changes take place over time. In other words, learning theories are grounded in assumed theories of time. These theories of learning would inform analytical choices made in temporal analysis---choices such as whether to focus on time-points or durations, changes over time or temporal organizations, timescales, reference points, and the relationship between temporal analysis and other analytical angles.

In addition to inspecting temporal assumptions embedded in learning theories, we also need to look at Given learning if often contextualized in an education regime and mediated by computer technologies,

-	Given time constraints placed by education regimes, the concern is to incur satisfactory “positive” changes in learners within a certain period of time. [How about no-change? Is it okay to stay unchanged?]

This speaks to, for instance, the context of MOOC and the notion of international classrooms (edX report) that have indeed blabla.

Education in particular has strict temporal boundaries that would dictate daily educational practice. Yet they are also usually implicitly assumed, just like our general relations to time at the individual and societal level.  Since the industrial age, we started to place learners into grade schools based on their age. Like other institutions, we slice up a calendar year into semesters or quarters, and divide a day into sessions for varied educational activities. In one class session, detailed planning is often championed and a “model” teacher may crush a session into minutes to demonstrate one’s dedication to education. In computer-supported learning environments, we implement sophisticated mechanisms to record timestamped learner activities; we build dashboards to present temporal graphs related to one’s progress in a domain. It seems in education we are also moving towards finer planning, monitoring, and controlling over our relation with time. Learning analytics as a field offers rich, exciting opportunities in this area. -->

## Moving forward

**There is an urgent need to (re)consider and reunite time and space in educational systems.** While many educational theories are fundamentally about time (e.g., Piaget's stages of cognitive development), there is increasing recognition of learning that happens in different spaces, places, and socio-cultural-political contexts.  Just like the reordering of time and space in modernization and globalization, the reordering of time and space has crucial implications for learning in our postmodern, postcolonial world. When building "powerful" tools like MOOCs and predictive analytics, we are inheriting -- often unknowingly -- older spatiotemporal structures that would dictate educational experiences of many. And of course, we're also creating new structures.

**Moving forward, one important exercise we could do is to reveal dominant views of time and space in our work at hand and ask some bizarre questions.** I don't know... Maybe asking:

- Are we making arrogant temporal assumptions about learners?
- How might the adopted temporal structure in our MOOC impact a learner from a different culture or speaking a different language?
- Is an analytics tool we build based on temporal analysis fair?
- How is a tool impacting the temporal aspect of learning?

Many of these questions are tough to answer. And we cannot expect algorithms or AI to address such questions. What questions do you have?


## References

- Chen, B., Knight, S., & Wise, A. F. (2018). Critical Issues in Designing and Implementing Temporal Analytics. Journal of Learning Analytics, 5(1), 1–9. https://doi.org/10.18608/jla.2018.53.1
- Edwards, R., & Usher, R. (2007). Globalisation & Pedagogy: Space, Place and Identity. Routledge.
- Knight, B., & Ma, J. (1993). Time representation: A taxonomy of temporal models. Artificial Intelligence Review, 7(6), 401–419. https://doi.org/10.1007/BF00849933
