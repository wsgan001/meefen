---
layout: post
categories: notes
title: 'Notes: Analyzing the flow of ideas and profiles of contributors in an open learning community'
tags:
- analytics
---

## References

**Citekey**: @halatchliyski2013

## References

Halatchliyski, I., Hecking, T., G\"ohnertTilman, & Hoppe, H. U. (2013). Analyzing the flow of ideas and profiles of contributors in an open learning community. In Proceedings of the Third International Conference on Learning Analytics and Knowledge LAK '13 (66). New York, New York, USA: ACM Press. doi:10.1145/2460296.2460311  












## Rough summary

The title of this article grasped my eyes. It appeared to be very relevant to what we're discussing about designing assessment of/for knowledge creation. Things we're interested include "how to evaluate idea rise," "how to identify metadiscourse moves," etc. The idea of tracing idea flow is definitely related to these topics.

The most important contribution of this paper, I think, is introducing scientometric methods into analyzing learning/knowledge building processes. It's actually not rocket science as it sounds like. The main thing in this method is its combination of social network and temporality. Using hyperlinks in a wiki (the case presented in this paper), the authors could build a network of artifacts, which are arguably regarded as ideas by authors. Then by laying out (revisions of) these artifacts on y-axis, temporal aspect is introduced in the analysis. After such a network (they call it "swim lane visualization") is constructed, they could conduct "main path analysis" to find out which nodes are in the main path. This can further determine which artifacts are playing important roles in the growth of knowledge, while others are less important or newer. When focusing on individual profiles, different types of authors become distinguishable. The authors define three types: workers, collectors, and initiators, which represent three different roles.

The technique of "main path analysis" is quite inspiring for thinking of assessment for knowledge creation. The trickiest parts, I think, are to define ideas, and links between them. The authors directly uses each wiki page to represent an idea; and we can do the same thing for analysis of Knowledge Forum data---using KF note to denote idea. This is quite natural but may need further scrutiny. For links, while hyperlinks in a wiki could be abundant, links in KF (including building-on, referencing, and contains) could become scarce in some cases. Referencing links are most close to the links used in scientometrics and this paper, but they're usually scarce in student notes. Building-on links are useful for analyzing idea flow, but they will produce a tree-like or divergent structure, which makes main path analysis not meaningful (because the structure is not a network but a tree). Combining those different types of links could be possible, but again, it depends on the nature of links available in a specific KF database. Other options include "secondary" links such as those based on shared vocabulary as introduced by KBDeX. It will be interesting to further explore different possibilities.

Anyway, I think the main path analysis mentioned in this paper is interesting and promising for assessment for knowledge creation.
## Clippings
Scientometric methods are tailored for the analysis of knowledge artifacts,  most  prominently  publications,  and  their  authors.  One well-known method is the calculation of the h-index as a measure of  scientific  reputation  [13].  In  the  context  of  learning communities,  however,  individual  excellence  is  not  a  primary concern.  Rather  more  interesting  would  be  an  approach  to  the long-term characteristics and the dynamics of interactive learning environments. (p. 1)

Hummon and Doreian [14] have proposed a method to detect the main  idea  flows  based  on  citation  networks  using  a  corpus  of publications in DNA biology as an exemplar. Our work reported in this paper takes this method, namely main path analysis, as a starting  point (p. 1)

The philosophical foundation of this view dates back to  Popper  [18],  who  explains  the  development  of  scientific knowledge as a constant process of emergence of new ideas and their  gradual  improvement  or  abandonment  after  discovering contradictory  evidence. (p. 1)

the temporal dimension should be regarded as a main component of  learning  analytics (p. 2)

Nevertheless,  the  field  of  learning analytics  still  needs  a  method  to  address  the  temporality  of learning processes quantitatively. Aspects that have to be further kept  into  account  include:  who  influenced  whom,  which  ideas were  taken  up  in  later  stages  and  which  were  not,  and  how differently  do  the  participants  contribute  to  the  overall  learning process. (p. 2)

However,  the  modeling  of  the  overall process of knowledge development is challenging, as it should be kept track of the sequential relations between all the changes in the knowledge base. Any aggregation across time easily leads to a biased  analysis  of  individual  and  community-level  variables.  A longitudinal  study  of  different  points  in  time  is  also  an unsatisfactory  option,  as  it  misses  out  the  authorship  of  the changes  that  have  been  made  between  the  chosen  time  points. Especially difficult is to grasp the nonlinear flow of ideas that is characteristic of any learning process. (p. 2)

From  the  systemic  view  of  the  co-evolution model  of  individual  learning  and  collaborative  knowledge building  [5],  a  community  and  the  participating  individuals function as two different types of systems that co-evolve through mutual  fertilization. (p. 2)

the basis of the relation between the actor (or author) and the artifact (or product) (p. 3)

3.2  Main path analysis (p. 3)

Temporality is explicitly accounted for through  the  very  definition  of  a  directed  acyclic  graph  (DAG) where nodes are single publications and directed edges represent citations  between  publications. (p. 3)

The main path can be described as the most used path in a citation network  taking  all  possible  paths  from  the  source  nodes  to  the sink  nodes. (p. 3)

Starting at the fictive source node, the main path is identified by successively  following  the  edge  with  the  maximal weight to the next  node  until  the  fictive  sink  node  is  reached. (p. 3)

This  paper  employs  the  search  path  count  (SPC)  algorithm  [2] that introduces one virtual source node and one virtual sink node and  links  these  to  each  of  the  actual  source  and  sink  nodes, respectively. (p. 3)

In  the  citation  network  of  scientific  publications  within one field, often one important publication is chosen as a starting point of the development of the field. This publication represents the  first  source. (p. 3)

The main path analysis  [14] is a network analysis technique for the  scientometric  study  of  scientific  citations  over  a  period  of time. (p. 3)

Using simple matrix operations such bi-partite two-mode-networks can be “folded” into homogeneous (one-mode) networks. Here, e.g., two actors would be associated if they have acted upon the same artifact. (p. 3)

SNA has been criticized for eliminating  time. (p. 3)

As a next step, a directed acyclic graph is constructed describing the complete flow of knowledge within a single domain in a wiki. Networks  of  hypermedia  resources  in  a  wiki  are  analogous  to networks of publications that are interconnected by citations. (p. 4)

This approach suggests using page revisions instead of wiki pages as nodes  in  a  DAG  extracted  from  a  wiki  data.  We  distinguish between two types of directed edges in such graphs: update edges and  hyperlink  edges. (p. 4)

multiple  main paths analysis [16]. (p. 4)

In order to visualize the main paths of idea flows in a wiki we use the visual metaphor of a swim lane diagram introduced in Figure  2. (p. 5)

knowledge flow between two wiki artifacts is established once by the initiating act of a hyperlink creation between them. (p. 5)

differences  in  the  contribution  activity  of  authors  that  can  be interpreted  in  terms  of a division of roles of contribution (p. 6)

specialized in linking articles and emphasize the relations  between  different  topics.  They  can  be  regarded  as “collectors” (p. 6)

Isolated  and largely unimportant articles are not part of the main path (p. 6)

“initiators”,  who  create  important  article revisions that are often referred by other articles later on. (p. 6)

performing  many  successive  revisions and probably creating the largest amount of content in the article. We call them “workers”. (p. 6)

4.4  Author profiles (p. 6)

ongoing  EU  project  “SISOB” 3   which has the goal to measure the influence of science on society based on  the  analysis  of  (social)  networks  of  researchers  and  created artifacts. (p. 7)

The  analysis  processes  described  in  this  paper  have  been integrated into our network analytics workbench. (p. 7)

It  appears  to  be  promising  to provide  moderators,  teachers,  tutors  or  the  productive  teams themselves  with  results  of  such  analyses,  in  order  to  support reflective  practices  [22]. (p. 8)
