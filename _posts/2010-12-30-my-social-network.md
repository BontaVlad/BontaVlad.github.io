--- 
layout: post
title: "My Social Network: A Simple Connected Graph"
tags: social-network 
---

The image here is my Facebook social graph; with my friends,
my friends of friends and so on as the vertices connected by edges representing their Facebook
friendships, limited only by members' individual privacy options. You can click on it
(a better idea would be to right-click and then do a "Save Link As") to open a 32MB ultra
high-res .png file where you can actually zoom in to read the names and stuff.

[![My Social Network](/images/social-network.jpg)][highres]

The graph's split up into dense clusters of friends, corresponding to my current college,
junior college and school. An interesting thing I noticed was Varun Vaswani, Chinmay Deshpande,
Kunal Bhatia and Prashant Sriram happen to be my *bridge vertices*; if all four of them somehow
just disappeared, or never existed, there would be no connection between my Facebook friends at
Goa (The bottom BITS Goa cluster) and at Bangalore (the top-left Deeksha cluster and the
top-right VNS cluster). I guess we're all special and indispensable to each other in some way.

The image was generated using a slight mod of the very intuitive
[fbfriendsgraph script][fbfriendsgraph].

[highres]: http://halfclosed.files.wordpress.com/2010/12/socialgraph.png
[fbfriendsgraph]: https://launchpad.net/fbfriendsgraph
