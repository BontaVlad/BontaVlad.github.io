---
layout: page 
homepage: true
permalink: /recommenders/jyoti/
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

Hi Jyoti,

Thank you for supporting my PhD applications!

You can find below a summary (of what I remember) of my time at Yahoo!, my
current research, and some other details you may find relevant
for your recommendation letters. The links on the left have more
general information about what I have worked on in the past.

## Yahoo!

### Summary

   * *Building systems:* Helped setup the initial Sipper sandbox. Contributed to
     Timesense on Storm. Built and evaluated the streaming content deduplication
     prototype (LSH) with Mridul. Implemented and deployed the Timesense Trending
     Tickers system.

   * *Analysing systems:* Analysed the CatSys categorization process and compared
     its results with Timesense. Evaluated the effect of reducing the Timesense
     candidate set. Studied the intricacies of HBase storage on disk
     and analysed different schemas, RPC batching parameters and block/scan sizes
     to improve the speed of restarting the topology.

   * *Scientific communication*: I gave a 3-hour tutorial at PyCon '13 on building a
      cluster with Beanstalkd. I submitted a poster to Techpulse '12 (with Jagrati,
      2 of 3 reviews were positive),
      and a paper to Techpulse '13 (with Hemanth). I also helped organize TechFM
      and gave a talk therein on random forests (had 30+ attendees). 

   * *Innovation:* I submitted to ID8 thrice: once as an intern
      and twice with Hemanth and Mridul. I also submitted 3 patent ideas, one of
      which (using Y! Messenger status messages for social music recommendations)
      received the go-ahead to be further refined. I began a periodic ideation process
      with Hemanth, and participated in many hackdays.

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

Here are some of the presentations I gave while at Yahoo!. The slides for all
my other presentations are [here](https://speakerdeck.com/emaadmanzoor).

   * Presentation given at TechFM:

<script async class="speakerdeck-embed" data-id="518d77e0a0da0130b8b42695b1cda53b" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

   * Presentation given at PyCon '13:

<script async class="speakerdeck-embed" data-id="5078db60cd52500002042a24" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

## Other Activities 

*Google Summer of Code 2014*

I was accepted by and awarded *$5,000 in funding* from Google to spend the summer of
2014 contributing to an open-source project for the Oregon State University.
[Less than 30% of the applicants](http://google-opensource.blogspot.in/2014/04/students-announced-for-google-summer-of.html)
were accepted into this programme.

*PennApps X Hackathon 2014*

I was selected to participate and awarded a *$500 travel grant* for the [PennApps X](http://2014f.pennapps.com/)
competition. Only [30% of the applicants](https://medium.com/pennapps-x/pennapps-x-application-stats-655f9a04f991)
were selected to participate, and 74 international travel grants were awarded,
out of 2360 applicants in total.

In the hackathon, I won the *Best Mashery Application* award out of 250 other teams,
which was sponsored by Intel.

*IEEE Xtreme 8.0 Programming Competition 2014*

I placed in the top 100 worldwide (out of 1720 teams), and rank 1 in the university and
region.

*Paper Reviewing*

I have reviewed papers for the following conferences and journals:

   * VLDBJ (1 paper)
   * CIKM 2014 (2 papers)

## Target Universities

<div class="table-wrapper">

**University** | **Deadline**
Stanford            | December 8
CMU                 | December 14
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
