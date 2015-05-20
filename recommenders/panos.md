---
layout: page 
homepage: true
permalink: /recommenders/panos/
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

Below you may find information about my research and coursework with you
so far, in addition to some other details.

## Current Research

For my thesis research, I am working on *scheduling broadcasts to maximize organic
reach in a network of timelines* ([early paper draft](https://docs.google.com/document/d/1ZpmqcH9hR4GvjTg99V56tCX41oxmXRO2nhBXYIfduM8/edit?usp=sharing)),
to be submitted to KDD 2015.

This work requires skills in theoretical modeling, data-driven analysis and validation,
and building real-world systems.

### Contributions

   * *Problem identification:* I surveyed literature and identified a research
      problem that is of interest to both the industry and academic community,
      which yields interesting insights, and for which a solution has not been
      attempted before.

   * *Novel insights and model:* The monotony aversion phenomenon, of users being
      annoyed when seeing too many posts by the same person, is quantified
      in this work for the first time. I am currently validating my formulation 
      on real data from Twitter. I have also validated the existence of rhythmic
      and bursty cycles in social network activity, which has not been done for
      microblogs before.

   * *Problem formulation and solution:* I have formulated the problem as a discrete
      optimisation task of constructing a user's timeline in the presence of competitors.
      The task works with a user model that encodes monotony aversion, information overload
      and bursty rhythmic behaviour. I am in the process of designing an efficient
      algorithm to solve it.

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

   * *The User Model:* We model social network users exhibiting information
      overload, bursty circadian rhythms and monotony aversion. We also formally
      define and quantify monotony aversion. This is the first such user model
      incorporating these behaviours.

   * *Model Validation:* We validate the effect of the different proposed
     formulations of monotony aversion, and also confirm the hypotheses of
     bursty circadian rhythms of microblog activity, and information overload.

   * *The Broadcast Scheduling Problem:* We introduce and formalize the
      broadcast scheduling problem with the aforementioned model. We then
      propose an algorithm to construct an optimal schedule.
  
   * *A Broadcast Scheduling System:* We build and deploy a real-world
      tweet scheduling system and evaluate its performance with the *@KAUST_News*
      account on Twitter, which has over 10,000 followers.

## Presentations

### Group Meetings

<script async class="speakerdeck-embed" data-id="ab72acf0c6330131e81c56974222b994" data-ratio="1.77777777777778" src="//speakerdeck.com/assets/embed.js"></script>
<script async class="speakerdeck-embed" data-id="01c52cc0525001329c82463548c09950" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

### CS341 Course

*Papers Presented*

   * Parallel Maximum Clique Algorithms
   * TurboISO: Fast Subgraph Isomorphism Search
   * GRAIL: A Scalable Index for Reachability Queries
   * R*: Optimizer
   * Schism: Workload-Driven Replication and Partitioning
   * Chord: Scalable P2P Lookup Protocol

*Slides*

<script async class="speakerdeck-embed" data-id="0f8ceba05636013284a72208fcc66d6d" data-ratio="1.77777777777778" src="//speakerdeck.com/assets/embed.js"></script>
<script async class="speakerdeck-embed" data-id="dd0a3a205636013284a82208fcc66d6d" data-ratio="1.77777777777778" src="//speakerdeck.com/assets/embed.js"></script>
<script async class="speakerdeck-embed" data-id="e3671ef056360132f59c3afb7544f96d" data-ratio="1.77777777777778" src="//speakerdeck.com/assets/embed.js"></script>
<script async class="speakerdeck-embed" data-id="7dd3e0f05634013284a82208fcc66d6d" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>
<script async class="speakerdeck-embed" data-id="d5570cb056360132f59c3afb7544f96d" data-ratio="1.77777777777778" src="//speakerdeck.com/assets/embed.js"></script>

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

At the hackathon, I won the *Best Mashery Application* award out of 250 other teams,
which was sponsored by Intel.

*IEEE Xtreme 8.0 Programming Competition 2014*

Placed 94th worldwide (out of 1720 teams).

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

### CMU
{:.no_toc}

[Database Group](http://db.cs.cmu.edu/) (*Note: Call for (+international) [interns](http://db.cs.cmu.edu/internship2015/)*)

People:

   * [Christos Faloutsos](http://www.cs.cmu.edu/~christos/): Graph mining.
   * [Andy Pavlo](http://www.cs.cmu.edu/~pavlo/): Databases.
   * [Eric Xing](http://www.cs.cmu.edu/~epxing/): Machine learning, social networks.

### Stanford
{:.no_toc}

[InfoLab Group](http://infolab.stanford.edu/)<br/>
[Hazy Group](http://i.stanford.edu/hazy/)

People:

   * [Jure Leskovec](http://cs.stanford.edu/people/jure/): Graph mining.
   * [Chris Re](http://cs.stanford.edu/people/chrismre/): Graph mining, machine learning, databases.
   * [Hector Garcia-Molina](http://infolab.stanford.edu/people/hector.html): Graph mining. 
   * [Jennifer Widom](http://cs.stanford.edu/people/widom/): Data management.

### Columbia
{:.no_toc}

[Database Group](http://www.cs.columbia.edu/database/)

People:

   * [Eugene Wu](http://www.mit.edu/~eugenewu/): Data visualization, exploration, management.
   * [Kenneth Ross](http://www.cs.columbia.edu/~kar/): Data management, hardware.
   * [Luis Gravano](http://www.cs.columbia.edu/~gravano/): Databases, information retrieval.

### Wisconsin-Madison
{:.no_toc}

[Database Group](https://database.cs.wisc.edu/)

People:

   * [AnHai Doan](http://pages.cs.wisc.edu/~anhai/): Data mining.
   * [Jignesh Patel](http://pages.cs.wisc.edu/~jignesh/): Data analytics, hardware.
   * [Jeffrey Naughton](http://pages.cs.wisc.edu/~naughton/): Databases.

### UCSB
{:.no_toc}

[Distributed Systems Lab](http://www.cs.ucsb.edu/~dsl/)<br/>
[Data Mining and Bioinformatics Lab](http://www.cs.ucsb.edu/~dbl/index.php)<br/>
[Systems, Algorithms, Networks and Data Lab](http://sandlab.cs.ucsb.edu/)<br/>

People:

   * [Amr Abbadi](http://www.cs.ucsb.edu/~dsl/?q=content/amr-el-abbadi): Graph mining.
   * [Ben Y. Zhao](http://www.cs.ucsb.edu/~ravenben/): Data mining.
   * [Xifeng Yan](http://www.cs.ucsb.edu/~xyan/): Graph mining.
   * [Divyakant Agrawal](http://www.cs.ucsb.edu/~agrawal/): Databases, graph mining.
   * [Ambuj Singh](http://www.cs.ucsb.edu/~ambuj/): Graph mining.
   * [Jianwen Su](http://www.cs.ucsb.edu/~su/): Databases.
   * [Tao Yang](http://www.cs.ucsb.edu/~tyang/): Information retrieval, parallel computing.

### UIUC
{:.no_toc}

[Data Mining Group](http://dm1.cs.uiuc.edu/)<br/>
[FORWARD Group](https://wiki.cites.illinois.edu/wiki/display/forward/Home)<br/>
[Data and Information Systems Lab](https://wiki.cites.illinois.edu/wiki/display/DAIS/Home)<br/>
[Text Information Management and Analysis Group](http://sifaka.cs.uiuc.edu/ir/index.html)<br/>

People:

   * [Jiawei Han](http://web.engr.illinois.edu/~hanj/): Graph mining.
   * [Kevin Chen-Chuan Chang](http://www-faculty.cs.uiuc.edu/~kcchang): Social networks, graph mining.
   * [Hari Sundaram](http://sundaram.cs.illinois.edu/): Social networks.
   * [Aditya Parameswaran](http://i.stanford.edu/~adityagp/): Visual analytics, crowdsourcing.
   * [ChengXiang Zhai](http://web.engr.illinois.edu/~czhai/): Information retrieval.

### Cornell
{:.no_toc}

[Databases Group](http://www.cs.cornell.edu/bigreddata/)

People:

   * [Johannes Gehrke](http://www.cs.cornell.edu/johannes/): Graphs, databases.
   * [Lucja Kot](http://www.cs.cornell.edu/~lucja/): Databases, transactions.

### Purdue
{:.no_toc}

[Indiana Centre for Database Systems](https://www.cs.purdue.edu/icds/doku.php)

People:

   * [Jennifer Neville](https://www.cs.purdue.edu/homes/neville/): Graphs, data mining.
   * [David Gleich](https://www.cs.purdue.edu/homes/dgleich/): Graph algorithms.
   * [Walid Aref](https://www.cs.purdue.edu/homes/aref/): Spatial databases.
   * [Sunil Prabhakar](https://www.cs.purdue.edu/homes/sunil/index.html): Data management, probabilistic databases.
   * [Luo Si](https://www.cs.purdue.edu/homes/lsi/): Information retrieval.

### Maryland
{:.no_toc}

[Database Group](https://www.cs.umd.edu/research-area/databases)

People:

   * [Amol Deshpande](http://www.cs.umd.edu/~amol/): Graphs, data management.
   * [Jennifer Golbeck](http://www.cs.umd.edu/~golbeck/): Social networks, user behavior/modeling.
   * [Jimmy Lin](http://www.umiacs.umd.edu/~jimmylin/): Social networks, user behavior/modeling.
   * [Louiqa Raschid](http://www.umiacs.umd.edu/~louiqa/): Social networks, data management.
   * [Hanan Samet](http://www.cs.umd.edu/~hjs/): Spatial data.
   * [Lise Getoor](http://www.umiacs.umd.edu/~getoor/index.shtml): Probablistic databases.

### Brown
{:.no_toc}

[Database Group](http://database.cs.brown.edu/)

People:

   * [Tim Kraska](http://cs.brown.edu/~kraskat/): Databases, machine learning.
   * [Ugur Cetinternel](https://sites.google.com/a/brown.edu/ugur-cetintemel/): Databases, streaming data.
   * [Stanley Zdonik](http://cs.brown.edu/~sbz/): Databases.

### Stony Brook
{:.no_toc}

[DataLab](http://www3.cs.stonybrook.edu/~datalab/)<br/>
[Data Sciences Lab](https://sites.google.com/site/datascienceslab/)

People:

   * [Leman Akoglu](http://www3.cs.stonybrook.edu/~leman/index.html): Graph mining (was a student of C. Faloutsos)
   * [Steven Skiena](http://www3.cs.stonybrook.edu/~skiena/): Text analytics, data mining, bioinformatics.
