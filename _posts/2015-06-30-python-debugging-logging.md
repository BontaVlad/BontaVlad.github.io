---
layout: post
title: Python debugging and logging
tags: debugging python logging
---
The world is great when everything goes according to plan, but as we all know, bad things are just around the corner.

---

##Just so you know
Good abstractions hide the complexity underneath, which is a good thing, but the downside of this is that when things go downhill we are left in the dark.
I wrote this article in the hope that it would help you when things inevitably don't go according to plan.

Contents
--------

* *Stage 1*: **Stack Trace** (the who, the what, the why)
* *Stage 2*: **Debugging** (techniques and tools, jk only print)
* *Stage 3*: **Python disassembler dis** (just because!!)
* *Stage 4*: **Logfiles**: creation/analysis (pretty pictures, I promise)

Stage 1: Stack Trace
-------------------
<img src="http://i.imgur.com/SrmsqoQ.jpg">

>If debugging is the process of removing software bugs, then programming must be the process of putting them in.
<br>
>Edsger Dijkstra (Dutch computer scientist, winner of the 1972 Turing Award)

If you ever wrote a line of code you most likely encountered a stack trace, event without knowing the exact name.
In simple terms, a stack trace is a list of method calls that the application was in the middle of when an Exception was thrown.

###Simple Example
In the following example an Exception was raised, by analyzing the stack trace we can determine where the Exception was thrown and possibly make an assumption abount what caused it.
To get started, lets consider the following Python script:


{% highlight python %}
def function1():
    raise RuntimeError('xxx')

def function2():
    function1()

def function3():
    function2()

def function4():
    fuction3()

def function5():
    function4()

{% endhighlight %}

The output of this script:

{% highlight python %}
Traceback (most recent call last):
  File "generate-1.py", line 16, in <module>
    function5()
  File "generate-1.py", line 14, in function5
    function4()
  File "generate-1.py", line 11, in function4
    function3()
  File "generate-1.py", line 8, in function3
    function2()
  File "generate-1.py", line 5, in function2
    function1()
  File "generate-1.py", line 2, in function1
    raise RuntimeError('xxx')
RuntimeError: xxx
{% endhighlight %}

This is a very simple stack trace. If we start at the end of the list we can see where our error happened.
But this could be misleading because the location where we cause the error might be different from the location where it originated.

1. Errors
2. Error paths
3. Async Paths

Stage 2: Debugging
----------------
<img src="http://i.imgur.com/vYALboG.jpg">

>Debugging is twice as hard as writing the code in the first place. Therefore, if you write the code as cleverly as possible, you are, by definition, not smart enough to debug it.
<br>
>Brian W. Kernighano (Canadian computer scientist, co-author of C programming language)

The scientific method goes something like this:

1. Identify the behavior you want to explain.
2. Form a hypothesis that might explain that behavior.
3. Conduct an experiment that tests the hypothesis.
4. If the experiment contradicts the hypothesis, revise it or replace it with a new hypothesis and go back to step 3.

Stage 3: Python disassemble dis
------------------------------
<img src="http://i.imgur.com/gFTx08h.jpg">

>Programming is like sex. One mistake and you have to support it for the rest of your life.
<br>
>Michael Sinz

Here at spyhce we had a recent discussion about cPython PyPy and Java and we realised that we had mixed understanding abount cPython's bytecode.
Since we are on the subject, let's clear some misinformation about this obscure subject.
I must mention, we are going to examine CPython interpreter bytecode limited to version 2.7, there are some differences between versions but the big ideas should hold.

We should spend a minute talking about what it means for a python program to be compiled since python is an intepreted language, (most languages that people think are not compiled, acctually have a compilation step just that the compiler does less and the interpretter is left with most of the work).
So python gets compiled to bytecode and the resulting bytecode(intermediary interpretation) is fed to the interpreter one instruction at a time.

{% highlight python %}
def mod(a, b):
    ans = a % b
    return ans
{% endhighlight %}

{% highlight python %}
# mod       <-- function
# func_code <-- bytecode
# co_code   <-- code object

mod.func_code.co_code   # func_code is not the same as bytecode
                        # bytecode is more leveled down
{% endhighlight %}

By running this we get this beauty

{% highlight python %}
'|\x00\x00|\x01\x00\x16}\x02\x00|\x02\x00S'
{% endhighlight %}

The bytecode is a series of bytes, so it looks weird here because some are printable and some are not.

We can make it a little better by looking at the ordinals for the printable and non-printable values

{% highlight python %}
[ord(b) for b in mod.func_code.co_code]
{% endhighlight %}

Here is the *better* version
{% highlight python %}
[124, 0, 0, 124, 1, 0, 22, 125, 2, 0, 124, 2, 0, 83]
{% endhighlight %}

We finally arrived at the magical **dis**. Dis is a bytecode disassembler which is included in python's standard library.
You want a disassembler any time you have assembly or low level code and you want to make it readable.
You will rarely see dis used in production but it's interesting to peek into python's internals.
{% highlight python %}
import dis
dis.dis(mod)
{% endhighlight %}
And the bytecode in all it's splendor:
{% highlight python %}
  3         0   LOAD_FAST               0 (a)
          3   LOAD_FAST    Z          1 (b)
          6   BINARY_MODULO
          7   STORE_FAST              2 (ans)

4         10  LOAD_FAST               2 (ans)
          13  RETURN_VALUE
#[1]      [2]   [3]                  [4] [5]

# [1] line number
# [2] index in bytecode
# [3] instruction name, for humans
# [4] more bytes the argument for each instruction
# [5] hint about the arguments
{% endhighlight %}

For more informations about this interesting subject you should really check [Allison's Kaptur](http://akaptur.com/about/) series about [Python-internals](http://akaptur.com/blog/categories/python-internals/).

Another excellent post by a guy named Romain [Understanding Python Bytecode](http://security.coverity.com/blog/2014/Nov/understanding-python-bytecode.html)

The name says it all [How fast can we make interpreted Python](http://arxiv.org/pdf/1306.6047v2.pdf)


Key concepts to take from this:

* **function objects**: these are the things people talk about when they say things like "functions are first-class citizens"
    this means that functions are objects and like any object we can talk to it without invoking it, we can pass it to another function as a argument, attach properties etc.
* **code objects**: generated by the Python compiler and interpreted by the interpreter.
    contains information about the job to be done: names of the variables, constants, and the number of arguments the function takes.
* **bytecode**: the interpreter will loop through each byte, look up what it should do for each one, the do that thing.
    the bytecode itself doesn't include any python objects, or references to objects, or anything like that.

----

If you came here thinking that dis will clear some of the hidden parts of python maybe you should check:

* [inspect](https://docs.python.org/2/library/inspect.html)
    a cousin of **dir()**
* [cinspect](https://github.com/punchagan/cinspect)
     is an attempt to extend Python's built-in inspect module to add "inspection" for Python's builtins and other objects not written in Python.


Cool links:

http://unpyc.sourceforge.net/Opcodes.html
souce codes for opcodes https://github.com/python/cpython/blob/master/Python/ceval.c
Dedicated lib: https://github.com/neuroo/equip

Stage 4: Logfiles (ELK stack)
------------------------------
<img src="http://i.imgur.com/NTmBLR1.jpg">

>If builders built buildings the way programmers wrote programs, then the first woodpecker that came along wound destroy civilization.
<br>
>Gerald Weinberg (American computer scientist)

###What is a logfile?

A logfile is the human readable, **machine parsable** representation of an event.

*Here you have a tipical apache server log entries:*
{% highlight bash %}
64.242.88.10 - - [07/Mar/2004:16:05:49 -0800] "GET /twiki/bin/edit/Main/Double_bounce_sender?topicparent=Main.ConfigurationVariables HTTP/1.1" 401 12846
64.242.88.10 - - [07/Mar/2004:16:06:51 -0800] "GET /twiki/bin/rdiff/TWiki/NewUserTemplate?rev1=1.3&rev2=1.2 HTTP/1.1" 200 4523
64.242.88.10 - - [07/Mar/2004:16:10:02 -0800] "GET /mailman/listinfo/hsdivision HTTP/1.1" 200 6291
{% endhighlight %}

All comes down to this: LOGFILE = TIMESTAMP + DATA

###What can you do with a logfile?

- Debugging
- Analytics
- Fraud detection
- Find abusive hot linking
- ...

###How can I read a logfile?
Opening it manually is difficult and error prone, disadvantage: can be only from
one source at a time
Huge files become impossible to handle.

###Remember the machine parsable part?
use grep: again single source, error prone, cryptic.
better methods stay tuned

###Meet ELS stack family

**Logstash - Collect, Enrich & Transport Data**

- Centralize data processing of all types
- Normalize varying schema and formats
- Quickly extend to custom log formats
- Easily add plugins for custom data sources

Here is a example of a ELS stack(some components may differ for you're setup)
<img src="http://i.imgur.com/2IxFtOH.png">

**Elasticsearch - Search & Analyze Data in Real Time**

- Distributed, scalable
- Real-time search and analytics capabilities

**Kibana - Explore & Visualize Your Data**

- Flexible analytics and visualization platform
- Real-time summary and charting of streaming data
- Intuitive interface for a variety of users
- Instant sharing and embedding of dashboards
