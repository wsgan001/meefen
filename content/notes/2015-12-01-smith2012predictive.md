---
layout: post
categories: notes
title: 'Notes: Smith. (2012). Predictive Modeling to Forecast Student Outcomes and Drive Effective Interventions in Online Community College Courses'
tags:
- learning analytics
- prediction
---

## References

**Citekey**: @smith2012predictive

Smith, V. C., Lange, A., & Huston, D. R. (2012). Predictive Modeling to Forecast Student Outcomes and Drive Effective Interventions in Online Community College Courses. Journal of Asynchronous Learning Networks, 16(3), 51–61.

## Notes

## Highlights


This is a case study from a community college utilizing learning analytics and the development of predictive models to identify at-risk students based on dozens of key variables. (p. 1)

The recent demands for increased student success efforts, most notably from the American Graduation Initiative [1], have come as colleges are facing limited funding and resources. The Associated Press [2] and the Center on Budget and Policy Priorities [3] have both recently highlighted the drastic budget cuts implemented by community colleges nationwide. Colleges are, therefore, charged with the task of developing new ways to respond to student needs with personalized, timely outreach efforts while simultaneously being mindful of resource limitations. (p. 1)

The 2011 Horizon Report produced by New Media Consortium and the EDUCAUSE Learning Initiative indicated that learning analytics will have a significant impact and forecasts its wide-scale adoption within the next five years [5]. (p. 1)

Rio Salado College (Rio) is located in Tempe, Arizona and is one of the ten colleges in the Maricopa County Community College District. (p. 2)

Online courses are delivered to students using RioLearn, a proprietary learning management system (LMS) that was built to serve over 100,000 students in partnership with Microsoft and Dell Computers. (p. 2)

As noted in the previous section, this research aimed to answer three primary questions. 52 Journal of Asynchronous Learning Networks, Volume 16: Issue 3 1. 2. 3. Which factors are effective as early or point-in-time predictors of course outcome in online learning? How can community colleges utilize those factors in predictive models to forecast student outcomes? How can community colleges utilize predictive models to implement proactive, effective, and sustainable student interventions with the goal of improving student success rates within the online learning population? (p. 2)

The data used for this study was collected from a freshman-level accounting course during the summer and fall 2009 semesters (p. 3)

Information pertaining to online student activity and assignment grades was obtained from RioLearn. Information pertaining to enrollments, including final grades, was obtained from PeopleSoft, the districtwide student information system used by the Maricopa County Community College District. (p. 3)

Logged in to RioLearn system Logged in to course section homepage Viewed the course syllabus Opened an assessment Completed an assessment Viewed grade book comments from instructor Viewed assessment feedback from instructor Opened a lesson Requested due date change Selected a custom calendar option (p. 3)

When analyzing LMS activity at multiple points in time throughout the duration of a course, we propose that recent behavior should be viewed with more significance than past behavior. (p. 4)

In keeping with this philosophy, we calculated the frequency of student activities as weighted sums based on when each activity occurred relative to the course start and end dates. (p. 4)

B. Naïve Bayes classification model (p. 4)

Ultimately, the naïve Bayes classification model was chosen because it offered significant advantages in several key areas compared to other methods. For instance, the naïve Bayes algorithm is computationally inexpensive, which is an important parameter due to the large student population at Rio Salado College. Also, Naïve Bayes is very scalable, meaning that the addition of more students or input variables will not cause a dramatic reduction in performance. Finally, as mentioned previously, naïve Bayes has demonstrated a strong record of accuracy in a variety of domains over many years of academic research [15, 16]. (p. 4)

A simple three-level warning indicator was used to provide a user-friendly abstraction of the estimated probability of course success—meaning a grade of “C” or better. The warning levels were labeled as Low, Moderate, and High. (p. 5)

Students with an estimated probability of success below 30% were determined to have a High warning level. Students above 70% had a Low warning level and students between 30% and 70% had a Moderate warning level. (p. 5)

C. Investigation of Factors (p. 5)

> weak correlations  
 these correlations are all pretty low, < .3. (p. 6)

D. Predictive Models (p. 7)

On average, the highest success rate was found in the Low warning group and the lowest success rate was found in the High warning group. The mean success rate was approximately 70% in the Low warning group, 54% in the Moderate warning group, and 34% in the High warning group. Therefore, the models were successful in accurately assessing the likelihood of successful course completion. (p. 7)

> accuracy questionable  
 Worse than a guess for high warning group? Why? (p. 7)

RioPACE, an acronym for Progress And Course Engagement. RioPACE was designed to determine appropriate warning levels on a weekly basis using updated activity and grade information. It was also intended to provide additional, more specific information to show student performance in the areas of log-in activity, site engagement, and pace. The system was again designed to run within the RioLearn LMS. (p. 7)

D. Interventions (p. 9)

This study demonstrated the strong correlation that exists between LMS activity markers and course outcome, which has also recently been noted by other researchers [12]. We have shown that log-in frequency, site engagement, pace, assignment grades, and some non-LMS enrollment factors can serve as effective predictors of course outcome, even as early as the eighth day of class. (p. 10)

> Interventions were not successful, probably caused by the weakness of the model.
