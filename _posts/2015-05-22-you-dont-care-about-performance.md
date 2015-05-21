---
layout: post
title: You don't care about performance
tags: python performance
---

My take on python profiling, definitions, motives, tools, cavesets and a hands
on approach to profile a fictive car part shop.

---

You **don't** care about performance, before you rant at me and include my mother
in the conversation, answer some of these following questions:

- Do you test for performance?
- If you do, you do it in a automatic and repeatable manner?
- Do you track, analyze and categorize the results?

>If you indeed answered most of this questions, you could stick around for [part
>two](#part2) in which I try to play with some useful profiling tools like
>[locust.io](http://locust.io/), [django-silk](https://github.com/mtford90/silk/)
>or maybe you are curios to see the special
>[app](https://github.com/BontaVlad/django-sample-app#django-sample-app) that I build
>especially for this demonstration.  For the rest of you, read on.

Profiling is a **complex** topic, so my take on this is to split it in two
parts:

- [**Part one**](#part1) will be a superficial quick and general introduction to
profiling python, no pryor knoledge required<sup>[1](#f1)</sup>, I just want to make sure that we are on
the same page.

- [**Part two**](#part2) is where we get our hands dirty and simulate a workflow of profiling a
application. This part will require from you some advance topics, but fear not,
still accessible to most of the readers out there.

##<a id="part1" href="#part1">Part 1</a>

Profiling for performance<sup>[2](#f2)</sup>
--------------------------------------------

I've used the term *profiling* several times before but never said anithing
about it.

According to wikipedia:

> Profiling (computer programming) is a form of dynamic program analysis
> that measures, for example, the space (memory) or time complexity of a
> program, the usage of particular instructions, or the frequency and
> duration of functions calls. Most commonly, profiling information
> servers to aid program optimization.

The short version is: profiling allows you to see where you are
spending your time, it allows you to optimize your code in a intelligent
fashion, runs **almost** exactly the same code as in production. You can
easly<sup>[3](#f3)</sup> track entry/exit times for functions and helps you
build the bigger picture about the application.

**TD;LR;**

- How much of resource X<sup>[4](#f4)</sup> is used?
- How exactly this amount of X is spent?
- Looking for bottlenecks

Why do we profile python?
------------------------

Because (and it hurts by heart to say this) **cPython** is slow. Python is a
beautiful language, but the rumor spread around by jealous Java
programmers is sadly true.

So why not make Python faster?

Well, that is exactly what [PyPy](http://pypy.org/) is trying to do.

PyPy is a automated, runtime, profile-driven optimization a.k.a. JIT compiler,
because PyPy tries to tackle a non-trivial problem we are not quite there yet.
Even so, at the moment, computers still aren't powerful enough to restructure your
entire program to use a better suited algorithm for the job.

So until then we profile.

Why not optimize everything?
--------------------------

>Fast code is expensive

Well, this is exactly what the *wizards* of yesterday did, they wrote code in which
every cpu cycle, every piece of memory mattered, *controll everything* was
the name of the game. They had no other way.

But this level of care come at a cost, fast code is expensive because it takes effort
to write (*good*) fast code. It needs better algorithms, deep research into
approaches, diligent and focused effort.

>Fast code is hard to maintain

Smart code introduces *caches*, *lazy loading*, *parallelization*, *assumptions* and
*requirements*.

Much smarter code gets you to *"meta-programming obscure"*, code where nothing
you write is the code that runs.

Sure it's fast, but it is extremely slow to write, and slow to maintain.

We need fast but maintainable code, so we give up right?

**No**, we do *"Intelligent optimization"*.

Obligatory Quote

>"We should forget about small efficiencies, say about 97% of the time:
>premature optimization is the root of all evil.
>Yet we should not pass up our opportunities in that critical 3%" -Knuth

The trick here is to mess up only a small portion of the codebase,
while preserving the elegance of the whole.
Maintain nice flexibility and we ugly just the important 3%.

How to find the 3%?
------------------

>Why not guess? "I really understand my code"

Well probably you do, and probably most of the time you do a good job
but you are taking a bet with 1 in 33 chance of guessing right. Better to look
first.

--------

**Cool stuff**

1. [Profile for performance](http://pyvideo.org/video/1587/profiling-for-performance)
    *I stole a lot of information from this wonderful presentation*
2. [Advance Python Profiling](https://www.youtube.com/watch?v=DUCMjsrYSrQ)
    *Excellent presentation with tons of code examples*


**Footnotes:**

<p id="f1">[1] *well thats no quite true, you still need to know about concepts as: functions, modules, stack*</p>
<p id="f2">[2] *here we cheat and say that the system is performant if it
satisfies some conditions, usually given in the
code specifications.*</p>
<p id="f3">[3] *well ussually not that easly but you get the point*</p>
<p id="f4">[4] *X can be CPU time, RAM, I/O, power*</p>
