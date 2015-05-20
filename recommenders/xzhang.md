---
layout: page 
homepage: true
permalink: /recommenders/xzhang/
---

<aside>

## quick facts
{:.no_toc}
*Current GPA:* 3.95/4.0<br/>
*([Transcript](/MS_transcript.pdf))*<br/>
*Department Rank:* 2<br/>
*GRE:* 1490/1600
   
   * 800/800 (Q)
   * 690/800 (V)
   * 5.5/6.0 (AWA)

*IELTS*: 8.5/9.0<br/>
*TOEFL*: Awaited<br/>
<br/>

## in this document
{:.no_toc}

* TOC
{:toc}

</aside>

Dear Prof. Zhang,

Thank you for considering recommending me for doctoral study.

You can find below some reports, presentations and other details about
my research and coursework with you so far. The links to the left of
the page contain more general information about my past projects.

## Past Research

### Summary

I worked on classifying malware Android applications using only
the permissions they request. I introduced the formulation of
reducing the dimensionality of the data using LDA, which gave
us insights into *types* of apps based on the *topics*
discovered by LDA.

### Weekly Progress

Below I have attached my reports and a bullet-point summary
of my work in each week.

*Week 2* ([Report](DirectedResearchWeek2.pdf))

   * Calculation and observations on PCA.
   * Calculation and observations on the pairwise permission correlation.
   * Introduced the first Latent Dirichlet Allocation formulation of the
     problem, initial results and classification performance with
     LDA + Naive Bayes.

*Week 3* ([Report](DirectedResearchWeek3.pdf))

   * Calculated correlation coefficients with p-values that were missing
     in the previous report.
   * Observations on the influence of app category on the permissions it
     requests.
   * Initial Bayes network design. 

*Week 4* ([Report 1](DirectedResearchWeek4.1.pdf), [Report 2](DirectedResearchWeek4.2.pdf))

   * Formulated the SVM + LDA cross-validation procedure for different numbers of
     LDA topics and SVM parameter settings.
   * Plots and observations of the ROC curves of SVM + LDA on both the sampled
     and full dataset.
   * Initial study of supervised LDA.

*Week 5* ([Report](DirectedResearchWeek5.pdf))

   * Surveyed many extensions and applications of LDA to better understand how
     it can be adapted to our problem.
   * The report compares the characteristics of each LDA extension to our
     problem, and discusses possible ideas for the next steps.

*Week 6* ([Report](DirectedResearchWeek6.pdf))

   * Evaluated k-means clustering on the 50-topics dimensionally reduced
     LDA data using homogeneity, completeness and V-measure.
   * Manually labelled LDA topics to observe their relation to application
     *functions*.
   * Noted an application *type* as a higher-level representation of functions,
     and studied hierarchical graphical models as a possible solution.
   * Surveyed better ways to directly evaluate the performance of LDA, rather
     than using SVM performance as a proxy.

## Current Research

For my thesis research, I am working on *scheduling broadcasts to maximize organic
reach in a network of timelines* ([early paper draft](https://docs.google.com/document/d/1ZpmqcH9hR4GvjTg99V56tCX41oxmXRO2nhBXYIfduM8/edit?usp=sharing)).
I am also the sole student working on this project, including the coding,
mathematical modelling, algorithm design and paper writing.

### Contributions

   * *Problem identification:* I surveyed literature and identified a research
      problem that is of interest to both the industry and academic community,
      and for which a solution has not been attempted before.

   * *Novel insights:* The monotony aversion phenomenon, of users being annoyed when seeing too many
      posts by the same person, is studied and quantified in this work for the first
      time.

   * *Real-world data:* I was able to connect with the CEO of a Twitter follower
      analysis company and persuade him to collaborate, thus obtaining Twitter
      unfollow data which is tracked by very few companies
      (Twitter itself does not).

   * *User modelling:* I have constructed a novel model of social network users
      and am in the process of validating my hypotheses on large datasets from
      Twitter (initial experiments are in the draft).

   * *Problem formulation/solution:* I have formulated the problem as a discrete
      optimisation task, of constructing a stream in the presence of competitors.
      I am in the process of designing an efficient algorithm to solve it.

   * *Real-world system*: I plan to build a real-world tweet scheduling system
      and evaluate it on the *@KAUST_News* Twitter account, which has over 10,000
      followers.

### Extended Abstract

In a typical social network, actions taken by users are *broadcast*
and appear on their friends' *timelines*. Timelines may be ordered chronologically,
as in Twitter and Instagram, or ordered by a mixture of recency and social metrics,
as in the Top Stories timeline in Facebook.

As a user in the network, one would like to produce posts to maximize *organic reach*,
which is the number of different users who view that post in the network.

Influenced by daily routine and the human sleep-cycle, social network users exhibit
a periodic and bursty usage pattern, and suffer from *information overload*.
Bursty users login to the social network once or twice a day, with their next
login separated by a long gap due to sleep or work.
Overloaded users consume their timelines only partially from the top downwards,
paying lesser attention to content appearing lower.

Hence, posts produced must be carefully scheduled to appear near the top of each
friend's timeline, or risk never being seen.

A naive solution to this is to flood the network by producing posts at a very
high rate. However, this would result in increased irritation and possible
unfriending or unfollowing. I call this phenomenon *monotony aversion*.

How can one then produce posts to maximize the organic reach, by maintaining a
balance between the varied sleep-cycles and tolerances to irritation of different
users?

This question motivates the following contributions in this work:

   * *The User Model:* I will construct a model of users exhibiting information
      overload, bursty circadian rhythms and monotony aversion. I will also formally
      define and quantify monotony aversion. This is the first such user model
      incorporating these behaviours.

   * *Model Validation:* Information overload has been studied and validated in
      prior research. I have validated the bursty circadian rhythms hypothesis on a
      large dataset from Sina Weibo. I will formally define and quantify monotony aversion, and
      validate its existence on a large Twitter dataset.

   * *The Broadcast Scheduling Problem:* I will introduce and formalize the
      broadcast scheduling problem with the aforementioned model. Then I will
      design an algorithm to construct an optimal schedule.
  
   * *A Broadcast Scheduling System:* I will finally build and deploy a real-world
      tweet scheduling system and evaluate its performance with the *@KAUST_News*
      account on Twitter, which has over 10,000 followers.

## Presentations

The following were presented by me in classes offered by you at KAUST. My other
talks are also available [here](/#talks).

   * I presented *Finding Communities in Networks* for the CS340 Data Mining
     course offered in Fall 2013.

<script async class="speakerdeck-embed" data-id="3cbb24b0359b013153d65efb0e8c9625" data-ratio="1.77777777777778" src="//speakerdeck.com/assets/embed.js"></script>

   * I gave a lecture *Reinforcement Learning* for the CS229 Machine Learning course
     offered in Spring 2014. I also prepared [notes](https://www.dropbox.com/s/2aj4tkwntrmddpx/CS229-RL-Notes-Emaad.pdf).

<script async class="speakerdeck-embed" data-id="6fba0c90be9a0131474766935fc535a5" data-ratio="1.77777777777778" src="//speakerdeck.com/assets/embed.js"></script>

   * I presented my machine learning course project on *Time Sensitive Network
     Inference in Continuous-Time Diffusion Networks* in Spring 2014.

<script async class="speakerdeck-embed" data-id="20c84bc0be990131474566935fc535a5" data-ratio="1.77777777777778" src="//speakerdeck.com/assets/embed.js"></script>

## Other Activities

*Google Summer of Code 2014*

I was accepted by and awarded *$5000 in funding* from Google to spend the summer of
2014 contributing to an open-source project for the Oregon State University.
[Less than 30% of the applicants](http://google-opensource.blogspot.in/2014/04/students-announced-for-google-summer-of.html)
were accepted into this programme.

*PennApps X Hackathon 2014*

I was selected to participate and awarded a *$500 travel grant* for the [PennApps X](http://2014f.pennapps.com/)
competition. Only [30% of the applicants](https://medium.com/pennapps-x/pennapps-x-application-stats-655f9a04f991)
were selected to participate, and 74 international travel grants were awarded,
out of 2360 applicants in total.

In the hackathon, I won the *Best Mashery Application* award out of 250 other teams,
that was sponsored by Intel.

*IEEE Xtreme 8.0 Programming Competition 2014*

I placed in the top 100 worldwide (out of 1720 teams), and rank 1 in the university and
region.

*Paper Reviewing*

I have reviewed papers for the following conferences and journals:

   * VLDBJ (1 paper)
   * CIKM 2014 (2 papers)

*Twitter Data Grant*

I helped write the proposal for the first [Twitter Data Grant](https://blog.twitter.com/2014/introducing-twitter-data-grants)
offered in 2014. However, we were not among the 6 research projects selected for the grant.

## Target Universities

<div class="table-wrapper">

**University** | **Deadline**
CMU                 | December 2
Stanford            | December 8
Columbia            | December 14
Wisconsin-Madison   | December 14
UC Santa Barbara    | December 14
UI Urbana-Champaign | December 14
Cornell             | December 14
Purdue              | December 14
U Maryland          | December 14
Brown               | December 14
SUNY Stony Brook    | January 14

</div>
