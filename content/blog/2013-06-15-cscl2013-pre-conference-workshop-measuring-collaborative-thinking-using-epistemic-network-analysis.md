---
date: '2013-06-15'
title: "#CSCL2013 pre-conference workshop: Measuring Collaborative Thinking Using
  Epistemic Network Analysis"
categories:
- blog
published: true
---

Today I've participated in a wonderful full-day workshop about Epistemic
Network Analysis (ENA), which I had been wishing to learn for a long
time. David and Gol did a great job explaining its theoretical
background, walking through a bunch of mathematical computation behind
it, and doing some interesting demos with some real data from their
research project. I had a great time playing with the sample data with
my "teammate" [Alisa](https://twitter.com/OhMissAcosta), and will
definitely apply it on some Knowledge Forum data in the near future.
It's also interesting that the system is based on R, and it makes me
seriously thinking about the possibility of building KF analytics on R.

![ENA](http://www.edgaps.org/gaps/wp-content/uploads/ENA_logo_web_sm.jpg)

I am posting my notes below. For more information about the workshop,
check [conference
website](http://www.isls.org/cscl2013/pre-conference-sessions.html)

Intro by [David Shaffer](https://twitter.com/DWShaffer): Measure collaborative thinking with ENA
------------------------------------------------------------------------------------------------

-   [David's slides](http://www.slideshare.net/dws1d/lak-05)

### Theoretical background of ENA

-   Its roots in research of epistemic games. Show video about the
    epistemic game for engineering education
-   Data mining --\> Data geology (data mining is a problematic term;
    have to understand the underline structure before digging into the
    data)
-   the need for 21st century thinking
-   community of knowledge ---| culture, knowledge, skills, values,
    identity; shared epistemology is important for a community
-   Shawn's research on creative community; reflection-on-action (pretty
    inspiring for my work on promisingness)
-   ENA aims to understand the structure of skills, knowledge, identity,
    values and epistemology.
-   go beyond psychometrics work focusing on specific skills. this tool
    is generic, can be applied to anyplace where network (of coding
    categories / epistemic frames) is more important rather than
    individual components.

### Explanation of the tool, focusing on mathematical stuff behind it

-   get chat discourse from the engineering epistemic game
-   code each utterance
-   validate (alpha scores)
-   coded data ready -- matrix, binary (rather than proportional data)
-   define stanza -- this concept is very important, because it will
    decide how co-occurrences occur
-   build adjacency matrix, based on collapsing coding results in a same
    stanza
-   build adjacency vector, converted from adjacency matrix
-   decide the unit of analysis - student, group of students, or else?
-   collapse stanzas for each unit of analysis, to get vectors for each
    unit
-   vectors represented by their directions, rather than positions
-   dimensional reduction (SVD) -- similar to Principal Component
    Analysis
-   each unit represented in a 3D space
-   making sense of reduced dimensions -- loading
-   this tool will not allow the analyzer to see a final position of
    each unit, but also its development trajectory.

My questions:

-   What assumptions are made in the stanza compression process?
-   What if frequency of epistemic frames are different? (also asked by
    another participant)

Thoughts

-   For the analysis of math discourse we are doing, counting appearance
    of different types of vocabs in students' utterance will basically
    give coded data of students' mathematical thinking. And then the
    tool can be applied. It will also be interesting to see the links
    between mathematical thinking and KB contribution.
-   Being able to see evolution of thinking is interesting.

Demos by [Golnaz Arastoopour](https://twitter.com/HeyItsGol)
------------------------------------------------------------

[Link to the ENA tool](http://epistemicgames.org/ena/)

-   The project started from Excel, and now its backend is based on R,
    and front-end visualizations are based on JavaScript
-   csv or R data; can be exported as R data to be further explored in
    RStudio

Questions and comments:

-   Given the larger number of plots to look at, how to find the most
    helpful plot?
    -   David: the reduced dimensions are ordered already by the
        percentage of variance.
-   This whole system is backed by R. Interesting way to develop LA
    systems.

Presentation by Chandra Orrill, University of Massachusetts Dartmouth
---------------------------------------------------------------------

General intro

-   work a lot on math education; focusing on teacher's professional
    development; proportional reasoning
-   diSessa's knowledge in pieces as hypothesis of her research
-   novice vs. expert teachers; experts focus on big ideas
-   importance of knowledge coherence for teachers

Study

-   interview data of teachers about proportional reasoning
-   7 teachers
-   Data coding
    -   Ratio concepts: iteration, ideas of growth, invariance,
        ratio-as-measure, ration calculation
    -   Fraction concepts: ...
    -   Problem solving: problem interpretation, verify math is correct,
        attend to context
    -   Representation: interpretation diagram, validate representation
    -   Other math ideas: ...
-   different patterns for different levels of teachers (stronger,
    middle, weaker)
-   adding more items (concepts?) into analysis will change results

Lessons learned

-   It helps to start small -- know data better
-   Not to be over-generous when coding -- be more strict when doing.
    "Do I see ... in this unit?"
-   Deal with codes that confound.

Questions:

-   Where I can access the R code that is used in RStudio?
-   What is a proper stanza for typical interview data? (Her answer is
    -- in her case, each teacher was asked to talk about a series of
    items. and discussion about one item was treated as a stanza. that
    makes sense!)

David presenting the process of going from raw data to ENA
----------------------------------------------------------

-   Example of analyzing Common Core standards
-   Important to make data reproducible; can go back
-   Be thoughtful in defining metadata, which is very useful for
    reproducing or reconstructing data
