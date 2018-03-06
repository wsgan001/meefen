---
date: '2015-05-02'
title: Mining frequent sequences in knowledge building dialogues
categories: blog
tags:
- analytics
- temporality
comments: true
summary: A demo of using Frequent Sequence Mining to uncover temporal patterns in knowledge building dialogues.
---

[![Out of Order](http://upload.wikimedia.org/wikipedia/commons/4/44/%27Out_Of_Order%27_by_David_Mach_-_geograph.org.uk_-_1102588.jpg)](http://upload.wikimedia.org/wikipedia/commons/4/44/%27Out_Of_Order%27_by_David_Mach_-_geograph.org.uk_-_1102588.jpg)

In a [previous post](blog/2014/04/17/temporailty-in-dialogues/) I highlighted the significance of studying temporality in collaborative learning and argued it should be studied more widely in learning sciences research because temporality matters for learning in a socio-cultural context. In the specific study I [presented](http://rpubs.com/bodong/lak14) at [LAK14](http://lak14indy.wordpress.com), an analytic technique named **Lag-sequential Analysis (LsA)** was applied to investigate sequential patterns among six **[contribution types](https://www.researchgate.net/publication/259178463_Ways_of_Contributing_to_an_Explanation-Seeking_Dialogue_in_Science_and_History)** in knowledge building dialogues by elementary school students. Such analysis was able to uncover temporal patterns that were otherwise undiscoverable using a traditional "coding-and-counting" technique, which is widely applied in many learning sciences studies. More methodological guidance is needed for the research community to make such technique accessible for more learning scientists.

### Introducing Frequent Sequence Mining

Later on when working on a MOOC research project at the University of Toronto, I got acquainted to another data mining technique named **[Sequential Pattern Mining](http://en.wikipedia.org/wiki/Sequential_Pattern_Mining)** or **[Frequent Sequence Mining ](http://en.wikibooks.org/wiki/Data_Mining_Algorithms_In_R/Sequence_Mining/SPADE) (FSM)**, which is a well-studied sub-domain of Frequent Pattern Mining. In a nutshell,

> Frequent Sequence Mining is used to discover a set of patterns shared among objects which have between them a specific order.

In my specific research context, because [knowledge building](http://ikit.org/kb.html) is conceptualized as an emergent process in which a community of people collectively improve their ideas by making various types of contributions to their discourse, the major question I was interested in was:

> to which extent do the sequential relations among different contribution types matter for effective knowledge-building dialogues?

So it became perfectly straightforward to apply FSM to the problem I was studying, with a hope that it could afford additional insights about temporality in knowledge-building dialogues.

### Data preparation for FSM

Note that I had two types of knowledge-building dialogues or conceptual **threads**: *effective* (or productive) and *improvable*. The first six rows of the thread data looked like this:

{% highlight r %}
> head(dft[, c(1, 3)])
                        thread type
1        HOW ARE ROCKS FORMED?    e
2 ROCK COMPOSITION AND TEXTURE    e
3                      FOSSILS    i
4                ROCKS COLOURS    e
5            Beginning of life    i
6 The creation of the universe    e
{% endhighlight %}

Each **note** (aka. post) in each thread was coded into six *contribution types*, including *questioning*, *theorizing*, *obtaining information*, *working with information*, *making synthesis and analogies*, and *supporting discussion*. Notes, after being coded, looked like this:

{% highlight r %}
> head(dfc[, c(2, 4, 5)])
                 thread noteid coding
1 HOW ARE ROCKS FORMED?      1      Q
2 HOW ARE ROCKS FORMED?      4      Q
3 HOW ARE ROCKS FORMED?      6      Q
4 HOW ARE ROCKS FORMED?      7      T
5 HOW ARE ROCKS FORMED?      9      T
6 HOW ARE ROCKS FORMED?     12     WE
{% endhighlight %}

To conduct FSM, a little bit of data transformation was needed to reorganize data into the following form:

{% highlight r %}
> head(dfc_e) # effective threads
    sequenceID eventID size items
460          1  100460    1     Q
461          1  100461    1     Q
462          1  100462    1     T
463          1  100463    1    WE
464          1  100464    1     T
465          1  100465    1     T
> head(dfc_i) # improvable threads
   sequenceID eventID size items
89          2  200089    1     Q
90          2  200090    1     T
91          2  200091    1     T
92          2  200092    1     Q
93          2  200093    1     T
94          2  200094    1    OE
{% endhighlight %}

Here, *effective* and *improvable* threads were partitioned into two separate tables with a same structure. To conform with the requirements of the [`arulesSequences`](http://cran.r-project.org/web/packages/arulesSequences/index.html) R package I was using, a thread was named a `sequence`, notes within it were represented as `events`, and coded contributions within a note were `items`.

### Running FSM on knowledge-building dialogues

After data were organized in this proper format, it became fairly easy to run FSM on each data partition using `arulesSequences`. There were a few parameters I could tweak to make the mining more meaningful for my specific research context (see code below). For instance, `maxgap` was (arbitrarily) set to 2, so two events with more than 2 events in between will not be captured in a sequence. Also, `maxlen` was set to 4, so sequences with more than 4 events will not be picked up. [`support`](http://en.wikipedia.org/wiki/Association_rule_learning#Useful_Concepts) was 0.1, so the analysis will pick up sequences that appear in at least 10% of a specific type of threads. More detailed explanation of these parameters could be found in arulesSequences' documentation.

{% highlight r %}
library(arulesSequences)
# read baskets
bskt <- read_baskets(file, info=c("sequenceID","eventID","SIZE"))
# mine frequent sequences
fs <- cspade(bskt, parameter = list(support = 0.1, maxlen = 4, maxgap = 2), control = list(verbose = TRUE, bfstype=TRUE))
{% endhighlight %}

After frequent sequences were identified for each type of threads, I was able to compare them to inspect whether there were sequences frequent for one type of threads but not for the other.

**Single-event sequence**

I started from comparing single-event sequences, i.e., single contribution types. Comparison of single-event sequences did not find any substantial difference between two types of threads. Apparently, *supporting discussion* and *working with evidence* happened more frequently in effective threads, but only for a bit more than 6% percent. Improvable threads had more frequent *making synthesis and analogies* contributions, and the difference was 11%.

{% highlight r %}
> Differentiate(fs_single_pretty, basket_files, 0.05)
  sequence effective improvable   diff
3    <{S}>      0.81       0.74  0.070
6   <{WE}>      0.48       0.42  0.063
4   <{SY}>      0.26       0.37 -0.110
{% endhighlight %}

These results to some extent triangulated with my LAK paper's finding that two types of threads did not significantly differ in percentages of contribution types, even though FSM only counted each contribution type's appearance only once and basic descriptive analysis could count multiple times.

**Multi-event sequences**

Comparing sequences with multiple events were expected to be more interesting. Here, I improved the `support` difference threshold to 20%. Results are presented below:

{% highlight r %}
> Differentiate(fs_multi_pretty, basket_files, 0.2)
              sequence effective improvable  diff
90   <{T},{T},{T},{T}>     0.839       0.42  0.42
88   <{S},{T},{T},{T}>     0.516       0.21  0.31
73   <{Q},{Q},{T},{T}>     0.645       0.37  0.28
282      <{T},{S},{Q}>     0.484       0.21  0.27
87   <{Q},{T},{T},{T}>     0.903       0.63  0.27
159 <{T},{T},{OE},{T}>     0.419       0.16  0.26
77       <{S},{T},{T}>     0.613       0.37  0.24
46          <{OE},{T}>     0.710       0.47  0.24
201  <{T},{T},{T},{S}>     0.548       0.32  0.23
81   <{T},{S},{T},{T}>     0.387       0.16  0.23
105  <{T},{Q},{S},{T}>     0.387       0.16  0.23
311        <{OE},{OE}>     0.387       0.16  0.23
65      <{OE},{T},{T}>     0.645       0.42  0.22
125      <{Q},{Q},{T}>     0.645       0.42  0.22
25  <{T},{T},{T},{WE}>     0.323       0.11  0.22
21      <{T},{T},{WE}>     0.419       0.21  0.21
74   <{S},{Q},{T},{T}>     0.419       0.21  0.21
79   <{Q},{S},{T},{T}>     0.419       0.21  0.21
133  <{T},{S},{Q},{T}>     0.419       0.21  0.21
240          <{Q},{Q}>     0.677       0.47  0.20
205     <{OE},{S},{S}>     0.097       0.32 -0.22
211  <{T},{S},{S},{S}>     0.097       0.32 -0.22
{% endhighlight %}

Generally speaking, in **improvable threads**, students more frequently responded to *obtaining evidence* or *theorizing* with *supporting discussion*, which was mostly about *giving opinion* on a contribution.

In **effective threads**, students had:

- more sustained *theorizing*, represented by several frequent sequences involving multiple `{T}`s
- more integrated use of evidence/information, represented by several frequent transitions between `{T}`, `{OE}` and `{WE}`, such as `<{T},{T},{OE},{T}>`, `<{OE},{T},{T}>`, and `<{T},{T},{T},{WE}>`
- and more frequent attempts to problematize proposed theories, represented by `<Q>` after `<T>`, as well as to propose explanations to solve problems, shown by transitions from `<Q>` to `<T>`

These results were consistent with what was found in the LAK paper using LsA:

> Effective dialogues require students to work more constructively with resources, engage in increasingly deepened questioning and theorizing, and problematize proposed explanations.

### Comparing FSM with LsA

In this experimentation, FSM and LsA arrived at similar results. However, there are noticeable differences. First of all, the underlying algorithms of them are quite different. While LsA relies on more basic matrix computation, the [SPADE](http://en.wikibooks.org/wiki/Data_Mining_Algorithms_In_R/Sequence_Mining/SPADE#Algorithm) algorithm implemented in `arulesSequences` was basically a process of searching and counting frequent sequences. In a sense, FSM is more flexible in picking up sequential patterns because it could tolerant event `gap` to be within a range, whereas LsA (at the version I used) could only configure `lag` to a specific value (e.g., 1).

In addition, because of the differences in computation, the results are also quite different. LsA could do significance tests, providing *p* values many researchers would like. In contrast, FSM produces values of `support` which can be compared among groups. It could also induce *association rules* from frequent sequences, to provide most sophisticated [*interestingness* measures](http://en.wikipedia.org/wiki/Association_rule_learning#Useful_Concepts), such as `confidence` and `lift`, for additional comparison.

### Conclusion

As two analytic techniques, both FSM and LsA focus on sequentiality of events so could be applied to study the temporal aspect of learning phenomena. My code for FSM is shared as a [Github gist](https://gist.github.com/meefen/7454d2fc8b9bc821c12a). Please feel free to tweak it to work with your own data. Since I am also learning FSM, corrections and comments are more than welcomed.
