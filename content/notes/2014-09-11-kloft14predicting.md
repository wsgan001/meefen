---
layout: post
categories: notes
title: 'Notes: Predicting mooc dropout over weeks using machine learning methods'
tags:
- MOOC
- learning analytics
---

## References

**Citekey**: @kloftpredicting

Kloft, M., Stiehler, F., Zheng, Z., and Pinkwart, N. (2014). Predicting mooc dropout over weeks using machine learning methods. In Modeling Large Scale Social Interaction in Massively Open Online Courses Workshop (EMNLP 2014).



## Notes

A potentially useful paper. The element of using historical features to predict dropouts is useful. It also built and tested a number of features for predicting dropouts. But the value of predicting dropouts in later weeks of a MOOC is limited.

## Highlights


While this problem is partially solved for students that are active in online forums, this is not yet the case for the more general student population. In this paper, we present an approach that works on click-stream data. Among other features, the machine learning algorithm takes the weekly history of student data into account and thus is able to notice changes in student behavior over time. (p. 1)

or instance, a linguistic analysis of the MOOC forum data can discover valuable indicators for predicting dropout of students (Wen et al., 2014). However, only few MOOC students (roughly 5-10%) use the discussion forums (Rose and Siemens, 2014), so that dropout predictors for the remaining 90% would be desirable. (p. 1)

we propose a machine learning method based on support vector machines for predicting dropout between MOOC course weeks in this paper. (p. 1)

The dataset we used in this paper was prepared for the shared task launched by the Modeling Large Scale Social Interaction in Massively Open Online Courses Workshop at the Conference on Empirical Methods in Natural Language Processing (p. 1)

According to the online data provided by Jordan (2014), most MOOCs have completion rates of less than 13%. (EMNLP 2014) (Rose and Siemens, 2014). (p. 2)

The data was collected from a psychology MOOC course which was launched in March 2013. The whole course lasted for 12 weeks with 11,607 participants in the beginning week and 3,861 participants staying until the last course week. Overall, 20,828 students participated, with approximately 81.4% lost at last. (p. 2)

After the post-processing the data consists of lists of attributes each correlated to a unique tuple consisting of the Coursera ID and the course week number. (p. 2)

2.1 Attributes description (p. 2)

Our model is an attempt to predict the participants’ drop-out during the next week (defined as no activity in that week and in any future week) using the data of the current and past weeks. (p. 2)

The complete attributes list is shown in Table 1. (p. 2)

For each line the corresponding Coursera ID is taken from the database (p. 2)

3 Methodology & Results (p. 2)

For each week i of the course, this results in a matrix X preliminary ∈ R19×ni , i the rows and columns of which correspond to the features and user ids, respectively. (p. 4)

> New note  
 not terribly clear about PCA here. Not sure why this is done. I was also left to guess that it was done on students.  
 SVM is not clear either to me. What data was used to predict the results here?? This part is really confusing. (p. 4)

PCA (p. 4)

The plot indicates that the users that have dropped out can be better separated from the users that did not drop out when the week id increases. (p. 4)

Box plots of these features showed that the distribution is highly skewed and non-normal, and furthermore all features are non-negative. We thus tried two standard features transformations: 1. logarithmic transformation 2. box-cox transformation. Subsequent box plots indicated that both lead to fairly non-skewed distributions. The logarithmic transformation is however much faster and lead to better results in later pipeline steps, which is why it was taken for the remaining experiments. (p. 4)

Subsequently, all features were centered and normalized to unit standard deviation. (p. 4)

we have made superior experiences with the Fisher score, which is why we focus on this approach in the following methodology. (p. 4)

ote that we found it beneficial to use the “history” features, that is the information about the previous weeks only within the weeks 1–12. For the weeks 13–19 we switched the history features off (also the PCA above is computed without the history features). (p. 4)

the video features (id 11–15), the most common request time (id 17), and the most active day feature (id 19) consistently achieved scores very close to zero, which is why they were discarded. (p. 4)

> Useful  
 Knowing some features are useful and some are not is very useful for future studies. However, we should be clear that these features were unuseful for this specific study but not for others probably. (p. 4)

> New note  
 Historical features are useful for predicting. This is useful to know. (p. 4)

The results indicate that features related to a more balanced behaviour pattern over the course of a week (especially the number of sessions and number of active days) were (weakly) predictive of dropout in the beginning of the course. (p. 4)

heart of our approach lies the extraction of numerical features capturing the activity level of users (e.g., number of requests) as well technical features (e.g., number of screen pixels in the employed device/computer). (p. 5)

We found the prediction is better at the end of the course, while at the beginning we still detect rather weak signals. (p. 5)
