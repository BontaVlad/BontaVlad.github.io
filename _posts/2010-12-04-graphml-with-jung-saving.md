--- 
layout: post
title: "GraphML With JUNG: Saving Out"
tags: jung
---

This one of two posts I'm dedicating to saving out to and loading from GraphML using the
JUNG library. These are two parts of a really good library that lack sufficient documentation.

{% highlight java %}
GraphMLWriter<MyVertex, MyEdge> graphWriter = new GraphMLWriter<MyVertex, MyEdge>();

PrintWriter out = new PrintWriter(new BufferedWriter(new FileWriter(filename)));
{% endhighlight %}

You first need to create your writers. The first line of code creates your
`GraphMLWriter` with your custom Edge and Vertex classes specified.

The next line creates a standard Java `PrintWriter`, which takes in input from a
`BufferedWriter`, which in turn is connected to a `FileWriter` that writes to the file
specified by the `String filename`. 

{% highlight java %}
graphWriter.addVertexData("x", null, "0",
    new Transformer<MyVertex, String>() {
        public String transform(MyVertex v) {
            return Double.toString(graphy.layout.getX(v));
        }
    }
);

graphWriter.addVertexData("y", null, "0",
    new Transformer<MyVertex, String>() {
        public String transform(MyVertex v) {
            return Double.toString(graphy.layout.getY(v));
       }
    }
);
{% endhighlight %}

By default, the XML file generated does not store the X and Y coordinates of the
vertices, so when you load a graph from a file, all the vertices are placed on top
of each other at a single point on the canvas. These are two bits of code that tell
my GraphMLWriter to add this information in to the file it creates.

The `addVertexData` function definition looks like this:

{% highlight java %}
public void addVertexData (String id,
                           String description,
                           String default_value,
                           Transformer<V, String> vertex_transformer)
{% endhighlight %}

The `id` is the string that I want added into my XML file, and is what I will be
using to extract the value while loading my graph from the file. The `description`
would describe the new data field you're adding, I've omitted that here. The `default_value`
is again a string, and the last argument is what makes it all work.

A `Transformer` can be looked as just something that transforms one object into another.
It has an abstract function `transform `that every transformer is required to implement.
In this case, the transformer is required to return a `String` that is needed by the
GraphMLWriter, and I've used my `AbstractLayout graphy.layout` to extract the X and Y
coordinates of the vertex and return them as strings to my GraphMLWriter.

{% highlight java %}
graphWriter.save(g, out);
{% endhighlight %}

This final bit of code saves out the `Graph g` using the `PrintWriter out`.
