---
layout: post
title: Micromotives and Macrobehavior
tags: behavioral-economics
---

The first chapter of [Micromotives and Macrobehavior][6] introduces the phenomenon
of people behaving in a self-serving way that results in some regular and predictable
pattern of the group's behavior as a whole.
 
An interesting question posed is, is there a relation between the
behavior characteristics of individuals and the characteristics of the aggregate?

More concretely, is it possible to,

   * Assume certain simple behaviors from the individuals, and predict the aggregate?
   * Observe the aggregate, and infer the individual behaviors that lead to it?

This is easy in many cases; for example, in a city where everyone drives home after
work, we can expect heavy traffic in the evening. What would make things complicated
is the fact that people may have *contingent* behavior, that depends on the
behavior of others around them.

For example, if people usually honk when someone else does, what would we
expect the decibel levels to be in different parts of the city? Could we use this
to better identify low-noise locations to construct hospitals at?

Another complication is that individuals acting selfishly, for their own interests,
may collectively create a situation in which nobody is happy. An interesting example
is [Braess's Paradox][8]:

![Braess's Paradox](http://upload.wikimedia.org/wikipedia/commons/0/01/Braess_paradox_road_example.svg)
*Braess's Paradox. [Source](http://commons.wikimedia.org/wiki/File:Braess_paradox_road_example.svg)*
{: style='text-align: center;'}

There are 4000 taxi drivers on the road network above, and they'd each like to get from
*START* to *END* as quickly as possible. The roads *START-B* and *A-END* take a fixed
45 minutes to drive through, but the roads *START-A* and *B-END* take time that is
dependent on the traffic *T* going through that road.

With every driver acting selfishly to minimize his driving time, what would the
traffic situation look like at equilibrium?

It turns out that at equilibrium, 2000 drivers take the *START-A-END* route and
2000 take the start *START-B-END* route, with each driver spending a total of
2000/100 + 45 = 65 minutes on the road.

The government steps in and decides to make things easier, by opening a high-speed
expressway from *A* to *B* that takes 0 time to drive through. How does this
affect the traffic situation?

Every driver first opts for the *START-A* road; this takes at most
 4000/100 = 40  minutes as opposed to 45 minutes by road
*START-B*. Then all drivers take the *A-B* expressway and the
*B-END* road, taking at most 0 + 4000/100 = 40  minutes, instead of
45 minutes if they'd taken the *A-END* road.

Each driver's travel time is now 80 minutes. Nobody will switch routes, because
the old *START-A-END* and *START-B-END* routes both take 85 minutes. Nobody is
happy. However, if every driver agreed not to take the *A-B* expressway, they would
all save 15 minutes on the road.

A bunch of research is taking place around such questions, from social scientists,
economists and even computer scientists. There is a certain pattern to this research,
that's also mentioned explicitly in the [Small-World Phenomenon][9] chapter in
[Networks, Crowds and Markets][5]:

   1. Perform a social experiment.
   2. Build mathematical models based on your observations.
   3. Make a prediction based on these models.
   4. Validate this prediction using real data.

If you find this kind of stuff interesting, a very good introduction is
the [Networks, Crowds and Markets][3] course by [Jon Kleinberg][2].

A new dimension to these questions that I came across
recently is neuroeconomics. Neuroeconomics too tries to understand human decision
making, but it pulls in perspectives from neuroscience. Concretely, it asks:

   * How can economic behavior shape our understanding of the human brain?
   * How can neuroscientific discoveries influence our economic models?

There is a [neuroeconomics course][4] starting soon on Coursera. An
interesting project would be to use the insights from this course to perform a
social experiment, build a more plausible model than what exists right now,
and validate it on data from Twitter or Facebook.

[1]: https://courses.cit.cornell.edu/info204_2007sp/
[2]: http://www.cs.cornell.edu/home/kleinber/
[3]: https://www.edx.org/course/cornellx/cornellx-info2040x-networks-crowds-1354
[4]: https://www.coursera.org/course/neuroec
[5]: http://www.cs.cornell.edu/home/kleinber/networks-book/
[6]: http://www.amazon.com/Micromotives-Macrobehavior-Thomas-C-Schelling/dp/0393329461
[7]: http://tembine.com/
[8]: http://en.wikipedia.org/wiki/Braess's_paradox
[9]: http://www.cs.cornell.edu/home/kleinber/networks-book/networks-book-ch20.pdf
