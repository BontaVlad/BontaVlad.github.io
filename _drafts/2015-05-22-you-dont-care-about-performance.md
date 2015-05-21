---
layout: post
title: You don't care about performance
tags: python performance
---

TODO: add description

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
profiling python, no pryor knoledge required just to make sure that we are on
the same page<sup>[1](#f1)</sup>.

- [**Part two**](#part2) is where we get our hand dirty and simulate a workflow of profiling a
application. This part will require from you some advance topics but still it
has some value, at least from an academic point of view.


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
fashion, runs almost exactly the same code as in production. You can
easly<sup>[3](#f3)</sup> track entry/exit times for functions and helps you
build the bigger picture about the application.

(?) Here is a basic profiler in python:
        t = time.time()
        try:
            function()
        finally:
            delta = time.time()
(?)

Enough with the general stuff, let's bring it more to home and talk about python
profiling.

Why do we profile python?
------------------------

Because (and it hurts by heart to say this) cPython is slow. Python is a
beautiful language, but the rumor that is spread around by jealous Java
programmers is sadly true. So why not make python faster?, that is exactly
what PyPy(link) is trying to do, PyPy is a automated, runtime,
profile-driven optimization a.k.a. JIT compiler, not a trivial problem by the
way, problem which requires a lot of time and money, stuff that PyPy needs the
most. Still, computers still aren't powerful enough to restructure your
entire program to use a better suited algorithm for the job.

So until then we profile.

So next logical question is:

Why not optimize everything?
--------------------------

>Fast code is expensive

Well, this is exactly what the wizards of yesterday did, they wrote code in which
every cpu cycle matters, every piece of memory counts, controll everything was
the name of the game. They had no other way.

But this level of care come at a cost, fast code is expensive, it takes effort
to write (good) fast code. It needs better algorithms, deep research into
approaches, diligent and focused effort.

    # Fast code is hard to maintain

Smart code introduces caches, lazy loading, parallelization, assumptions and
requirements.

Much smarter code gets you to "meta-programming obscure", code where nothing
you write is the code that runs.

Sure it's fast, but it is extremely slow to write, and slow to maintain.

We need fast but maintainable code, so we give up right?

No, we profile, and we do it in an analytical fashion, we do "Intelligent
optimization"

Obligatory Quote

>"We should forget about small efficiencies, say about 97% of the time:
>premature optimization is the root of all evil.
>Yet we should not pass up our opportunities in that critical 3%" -Knuth

So we mess up only a small portion of the codebase, while preserving the elegante
of the whole.
(?) maintain nice flexibility and we ugly just the important 3% (?)

Why not guess? "I really understand my code":
well probably you do, and probably most of the time you do a good job
but you are taking a bet with 1 in 33 chance of guessing right. Better to look
first.

How? Well this is the end of part 1.

--------

**Footnotes:**

<p id="f1">[1] *well thats no quite true, you still need to know about concepts as: functions, modules, stack*</p>
<p id="f2">[2] *here we cheat and say that the system is performant if it
satisfies some conditions, usually given in the
code specifications.*</p>
<p id="f3">[3] *well ussually not that easly but you get the point*</p>
