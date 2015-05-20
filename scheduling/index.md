---
layout: page
title: Scheduling Broadcasts in a Network of Timelines
homepage: True
permalink: /scheduling/
---

Supplementary information for our KDD '15 submission.

## Paper

[Preprint](2015.KDD.EmaadAhmedManzoor.pdf).

## Data

We use the [Twitter-Friends](http://linshuyang.com/research/PDC/) dataset described
in the following paper:

> Steering Information Diffusion Dynamically against User Attention Limitation.
> Shuyang Lin, Qingbo Hu, Fengjiao Wang, Philip S. Yu. ICDM ’14.

We provide Python [pickles](https://wiki.python.org/moin/UsingPickle)
of this data for convenient reuse in code:

   * `all_links.p` ([Download](all_tweets.p)): A list of tuples of user ID's,
     one for each link in the network, of the form *(a, b)* where *b* follows *a*.

   * `all_tweets.p` ([Download](all_tweets.p)): A list of tuples, one for each tweet,
     containing following information in order:

      1. Tweet creator ID.
      2. Tweet creation time (in milliseconds since the epoch).
      3. Retweeted user ID (-1 if not a retweet).
      4. Replied-to user ID (-1 if not a user-reply).
      5. The tweet ID.
      6. Retweeted tweet ID (-1 if not a retweet).
      7. Replied-to tweet ID (-1 if not a tweet-reply)

## Attention Potential

[Annotated code](https://gist.github.com/emaadmanzoor/a1e6632f905fa6bcbbcb).

Attention potential is a directed function *ap(a,b)*, estimating the attention that follower *b*
gives producer *a*. Likewise, reactions are also directed *reactions(a,b)*, measuring the number
of retweets to and replies of *a*'s tweets by *b*. The code linked above evaluates the correlation
between attention and reactions in the Twitter dataset.

## Monotony Aversion

[Annotated code](https://gist.github.com/emaadmanzoor/55f2b1c72764a2ba9bfd).

The code linked above computes statistics of author-occurence clusters.
For each cluster size, it reports the following:

   * The number of clusters of this size.
   * The number of tweets arising from clusters of this size.
   * The number of tweets reacted to in clusters of this size.
   * The number of clusters of this size containing at least one reaction.
