---
layout: post
title: Simple neural network written in Nim running on the web
tags: nim projects
comments: true
---

I've made a simple neural network in Nim based on a fantastic book by Tariq Rashid. Read on if you want to hear more on the implementation and play with the demo.

---


# The book

![img](//i.imgur.com/UC1meTs.jpg)

Great book! This is a nice introduction to neural networks. This book not only goes over the theory but also the step by step implementation. At the end you will have a simple neural network that recognizes handwritten numbers, all done with Python. This was the perfect candidate for practicing my nim-fu because this project has a low number of dependencies, relative simple math and clear, readable Python code.

The book touches on the subject of predicting machines, goes on explaining what a neuron means in the context of a neural network, why matrices are useful, what are weights and how does the actual learning process even work. The following chapters deal with the actual implementation, some python theory and extra things you can do with the nn once you've finished the project.

I will not go into many details about neural networks, Tariq Rashid does a much, much better job in his book. What I will do is give you a small context regarding the demo you are about to see.


# Overview

First of, we require some inputs nodes (neurons) so that the network can \`see\` the image, for each node we supply a pixel value, since we use 28 by 28 pixel image size, this means we need a total of **784** input nodes. 

The \`hidden\` nodes are the nodes where the actual learning process actually happens, each node connects with other nodes, but not all connections are the same, the weight of o connection determines it's importance, higher weight means greater importance. During the learning process we simply change the weights between the nodes to get closer and closer to the correct answer. More hidden layers we have, the more learning we can do (up to a point).

Lastly, we need to formulate an answer, since we deal only with numbers ranging from 0 to 9 we can use **10** output nodes, each one representing a digit, the biggest value of a node determines the \`winning\` node, the answer.

You can picture our neural network looking similar to this:
![img](//i.imgur.com/ckrX2V8.png)

Now that we have the network in place, in order for it to be useful we must train the 'beast'. For that I have used (as instructed) a dataset containing handwritten numbers, each having a corresponding label (the right answer). This is a sample taken from the data set. ![img](//i.imgur.com/oE8sJF7.png) You can check the whole lot [here](https://pjreddie.com/projects/mnist-in-csv/).

The learning process is as follows: let's say that the answer given by the network is `out` and the correct answer is `correct`. To get the error we will need to do some subtraction and multiplication: `error = (correct - out) * learning rate`. The answer will tell us how far we are from the correct answer. Learning rate determines the size of the steps we take towards minimizing the error. Choosing a good learning rate is important because is we chose one that is too small, the learning process is inefficient, the steps we take towards the goal are too small. Choosing a big learning rate is equally damaging because we risk overshooting and miss the answer altogether.

With the resulting error we must adjust each node's weight. We do that by starting from the output nodes going in reverse towards the input nodes, procedure aptly named back propagation. Using some math wizardry named [gradient descent](https://en.wikipedia.org/wiki/Gradient_descent), we get the new weight for each node.


# Implementation

In my case Python brings home the bacon (programming in Python is my job). For me working in a language that I enjoy was always my primary objective. While I will not ditch Python anytime soon, I chose to implement all my side projects in Nim because I either want to learn about some low level stuff like: pointers, memory management (if you chose to opt out from nim's garbage collector), concepts, etc or simply because I need/want raw speed without to much of a hassle. I like to play from time to time with a compiled, statically typed language and Nim is the best way to go in my case, I get the same fun factor as with Python without the speed penalty.

For implementing the neural network I chose a cool matrix library called [Neo](https://unicredit.github.io/neo/). Neo's goal is to become what Numpy is for Python programmers. It makes use of libraries such as ATLAS, OpenBlas, Intel MKL. It even provides GPU support using NVIDIA CUDA 8.0.

Neo's documentation and api were nice to work with and as a bonus I got multi-core support right off the bat. Training my neural network went smoothly and fast.

Once I finished the project I wanted to show it off on the internet. Here Nim's javascript back-end comes in handy (Nim supports multiple backends such as c, c++, objective-c and javascript). Since Neo uses external libraries, I had to chose another matrix module without external dependencies. The online version of the nn is pre-trained and that makes performance not a high priority anymore, javascript can handle some simple matrix operations, so [this](https://github.com/twist-vector/matrix) module fits the bill nicely.

For the HTML5 canvas bindings I chose [HTML5-Canvas-Nim](https://github.com/define-private-public/HTML5-Canvas-Nim). Interfacing with javascript from Nim only requires some function signatures and type declarations. Using HTML5-Canvas-Nim I got a working demo in no time.

To make things more easy, for the neural network I decided to use a bounding box around the drawing and resize only that to 28x28 pixels. This means that you can draw in any possition and almost any size and the network still gets a nice input image to work with. A demo of the code I have \`stolen\` is [here](http://phrogz.net/tmp/canvas_bounding_box.html) .

You can find all the source code here: [neural nim](https://github.com/bontavlad/neural_nim). Branch `master` is where I use the Neo module, and branch `js_matrix` is the code for the web demo.

My next challenge is to compile the network to WebAssembly. Here Nim shines again because of it's multiple compilation backends. You can compile to c/c++ and then WebAssembly for a huge performance gain, and compile to js the other parts of the application that deal with the dom or other javascript modules, with the advantage of having both parts in the same language.

As always, leave any constructive comments in the section below, and let me know if something is wrong, badly written, or maybe useless? I'm still new to Nim, neural networks, even article writing.

Happy hacking!

PS: You have a programming problem and think I could help? Hit me with an email at bonta.vladxxgmail.com (replace xx with @) and let's talk about it!


# Demo:

<script type="text/javascript" src="/js/neural_nim/main.js"></script>
<style type="text/css">
  canvas {
      border: 1px solid black;
      margin: 0px;
  }
</style>
<canvas id="surface" width="500" height="500"></canvas>
<h3>I think you drawn: <span id="sure"> --- </span></h3>
<h4>But it could be also: <span id="maybe"> --- </span></h4>
<button id="clear-btn" type="button">Clear canvas</button>
<button id="guess-btn" type="button">Guess!</button>
<button id="correct-btn" type="button">Correct Me!</button>
<input type="text" id="correct-input" name="usrname" size="1">

