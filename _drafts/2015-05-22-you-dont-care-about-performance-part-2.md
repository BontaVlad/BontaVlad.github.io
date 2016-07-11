---
layout: post
title: You don't care about performance (Part 2)
tags: python performance
---

Here we pick up where we left off in [part 1]
**WIP**

---

Since we already had the introduction, let's dig right in:

### Building blocks

As a warmup, we are going to start with something simple, but do not
underestimate the power of simple things.

#### bash ```time```

A perfect example for using time is on django managements commands. Let's try
to measure user ```harvest_name_populate_database``` from the [app].
{% highlight bash %}
$ /usr/bin/time -p ./manage.py harvest_name_populate_database

real 37.45
user 2.65
sys 0.40

{% endhighlight %}

What does the output of ```time``` tells us?

    real 37.45 -- wall clock time(from start to finish of the call)
    user 2.65  -- is the amount of CPU time spent in user-mode code
    sys 0.40   -- syscalls, memory allocation, I/O, etc.

That took long enough, ```37.45``` seconds to be exact, so in the future when calling
```harvest_name_populate_database``` will give it a handy
```--limit n``` parameter.

You might say that is pretty useless, but if you think about it, this already
tells you a lot, from a single glance you can tell if youre implementation is
*CPU* bound or *I/O* bound, how much it took and if you need it faster.
Time is perfect for triyng different algorithms and see realy quick which one is faster.

>Lesson 1. Sometimes less is more.

#### ipython ```timeit```

{% highlight bash %}
$ ./manage.py shell_plus
{% endhighlight %}

{% highlight python%}
from home.management.commands.harvest_name_populate_database import Command
%timeit Command().handle(limit=None)
1 loops, best of 3: 36.5 s per loop
{% endhighlight %}


#### python ```cProfile```
This will be the bread and butter from now on


Now that you know the building blocks for profiling the ? CarPartsShop, let's
proceed to profile it.

First stop:

Know when to profile
--------------------

# The big picture

#### locust.io

Profiling is hard, and this will sound strange comming from an article about
profiling, but if you can, do **NOT** profile. Profiling can be tricky, full of
cavesets, hard work with possible diminishing returns. Before starting make sure
you really have to do it.

Usually *good enough* is better than perfect, but how do we know what is good
enough. Well my friend, this is something that software requirements will tell
you, youre senior, boss, and at least the client.

Testing with a single user provides good information but it doesent assure you
that when things get hot, you will still manage to server the request at the
same response time.
So lets start to stress our application, simulation some user interaction.
locust is perfect for this because you can interact with youre appliation in a
repetable and predictable manner, and best of all, the scripting is done using
Python.

>Before we begin, make sure you run all locust commands using python 2.6+,
>python 3 is not yet supported, also if you don't want to kill youre pc, use
>gunicorn as a application server

Go to performance_test folder and start the locust server

{% highlight bash %}
$ locust --host=http://127.0.0.1:8000
{% endhighlight %}

If all goes well you can access the locust web inteface at
[127.0.0.1:8089](http://127.0.0.1:8089)


##### django-silk
add urls
add installed apps
add middleware
run syncdb
start runserver
clear old records if exists
play with the application
see results

### Module lever picture

#### PyCallGraph
install dependencies
run test
see resulting png


##### cProfile
import cProfile

attach code


## Visualize data
runsnake get_parts_list.prof
snakeviz get_parts_list.prof


### Method Level picture

##### line_profiler
##### pprofile
{% highlight bash %}
$ pprofile --out cachegrind.out.threads demo/threads.py
{% endhighlight %}









<br><br> <br><br> <br><br> <br><br>

--------
**Cool stuff**

1. [Profile for performance](http://pyvideo.org/video/1587/profiling-for-performance)
    *I stole a lot of information from this wonderful presentation*
2. [Advance Python Profiling](https://www.youtube.com/watch?v=DUCMjsrYSrQ)
    *Excellent presentation with tons of code examples*


**Footnotes:**

<p id="f1">[1] *not yet*</p>

[part 1]:http://time.is
[app]:https://github.com/BontaVlad/django-sample-app#django-sample-app
