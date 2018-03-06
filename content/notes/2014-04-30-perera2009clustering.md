---
layout: post
category: notes
tags:
- analytics
- temporality
title: 'Notes: Clustering and sequential pattern mining of online collaborative learning data'
---

## References

Perera, D., Kay, J., Koprinska, I., Yacef, K., & Zaïane, O. R. (2009). Clustering and sequential pattern mining of online collaborative learning data. Knowledge and Data Engineering, IEEE Transactions on, 21(6), 759–772.

**Citekey**: @perera2009clustering

## Notes

## Highlights


mirroring (p. 2)

To underpin our work, we have used the Big Five theory of group work [1]. (p. 3)

It has established five key factors: leadership, mutual performance monitoring, backup behaviour, adaptability and team orientation. (p. 3)

As a main clustering algorithm we selected k-means which is the most popular. It is also simple, effective and relatively efficient [20, 21]. We used the WEKA [22] implementation with Euclidean distance measure. (p. 5)

The most important problem was attribute selection. The performance of clustering algorithms is very sensitive to the quality of the attributes. (p. 5)

As shown in the previous section, simple statistical exploration of the data was quite limited. The results suggested the need to consider multiple data attributes simultaneously. Clustering allows us to use multiple attributes to identify similar groups in an unsupervised fashion. (p. 5)

Such results are useful for the course co-ordinator. They highlight that Group 1’s behaviour is distinguished from the others. The co-ordinators had some sense that this group was well managed but this cluster analysis pointed to the particular behaviours that distinguished this group. We only noticed these after the results of the data mining prompted us to look at particular parts of the TRAC sight and to see the way they used tickets. (p. 6)

This new understanding was used in subsequent teaching and was judged by the facilitators to be helpful. (p. 6)

Based on our interpretation of the characteristics in Table 6, a cluster label was assigned (“Managers”, “TRACoriented developers”, “Loafers” and “Others”). The distribution of students from each group into these 4 clusters is presented in Table 7 (p. 7)

There are two main approaches to sequential pattern mining: apriori-based [25] and pattern-growth methods [28, 29]. Both of them find the same results but the pattern growth approach is much faster. (p. 8)

An important aspect of our data which is ignored by mining techniques such as clustering is the timing of events. (p. 8)

A data mining technique which considers this temporal aspect is sequential pattern mining [25]. (p. 8)

:::New note  
 apparently, they run with a very low support and pick those ones showing greater difference.  
 so we do not necessarily need 50% of support.::: (p. 10)

We ran the GSP algorithm with a very low support threshold because when patterns are found to be frequent in one group, we need to compare this with the exact frequency in other groups where they are not frequent. (p. 10)

the best groups had many alternations of SVN and wiki events, and also SVN and ticket events whereas weaker groups had almost none. (p. 10)

Although the overall number of patterns found was very high (up to 40,000), only the ones that are frequent in at least one group and low in at least one other were retained, reducing easily that number down to a humanly manageable size of about 50. (p. 10)

In contrast, the least successful group displayed a high level of alternating wiki and ticketing events, but also had a distinctive lack of sequences containing SVN events. (p. 11)

the best group was one of only two groups to display the patterns (1tb)(1sb) and (1sb)(1tb) – the first likely being a ticket being accepted by a team member and then SVN work relating to that task being completed and the second likely being work being done followed by the ticket being closed. (p. 11)

the top group used the ticketing system more than the wiki, whereas the weakest group displayed the opposite pattern. (p. 11)

Another series of patterns which characterised the best groups were tickets being initiated by non-leader group members (p. 11)

A pattern which characterised the poorest group was the tracker creating and editing many tickets, for example in the patterns (1tT), (1tT)(1tb) and (2tT). (p. 11)

We found that the two top groups had by far the greatest percentage support for the pattern (1tL)(1tb), which were most likely tickets initiated by the leader and accepted by another team member. The fact that this occurred more often than (1tL)(2tb), suggests that the better groups were distinguished by tasks being performed on the wiki or SVN files before the ticket was closed by the (p. 11)

6.7 Limitations of Sequential Pattern Mining (p. 12)

We found that the top group had very high support for patterns where the leader interacted with group members on tickets, such as (L1t)(b1t)(L1t). (p. 12)

A problem with our mining program itself is the lack of gap constraints – as noted in [25], a frequent subsequence of (X)(Y) may not be meaningful if many other events occur between X and Y. Another issue is the need for more automated methods of processing output which go beyond manual sorting techniques. Emergent pattern mining [32] and contrast sets [33] may be possible solutions. Finally, there still remained the need to assign meaning to the patterns in order to learn about group work in general. The importance of finding the right balance between alphabets that are too abstract (limiting interpretation) and those which are too specific cannot be understated. (p. 12)

In addition, the best group displayed the highest support for patterns such as (b3t) and (b4t), suggestive of group members making at least one update on tickets before closing them. (p. 12)

this group also displayed higher than average support for patterns of interaction involving multiple team members, such as (b1t)(c1t)(L1t). (p. 12)
