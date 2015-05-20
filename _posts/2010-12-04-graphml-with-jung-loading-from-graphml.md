--- 
layout: post
title: "GraphML With JUNG: Importing GraphML"
tags: jung
---

This is a follow up to my  [earlier post]({% post_url 2010-12-04-graphml-with-jung-saving %})
on saving to GraphML using the JUNG library. It would make more sense if you browsed through
that post before reading this one.

{% highlight java %}
BufferedReader fileReader = new BufferedReader(new FileReader(filename));
{% endhighlight %}

You first need to read from your file. This snippet creates a standard Java `BufferedReader`,
which in turn is fed from a `FileReader` that reads from the file specified by the
`String filename`.

The problem is, the `GraphMLReader2` is just a smart text parser. For it to do anything useful,
you need to specify `Transformers` for the vertices, edges, hyperedges and the graph itself.
We pump these transformers into the function reading the graph so it understands what exactly
to do after it reads these different components in from the GraphML file.

{% highlight java %}
/* Create the Graph Transformer */
Transformer<GraphMetadata, Graph<MyVertex, MyEdge> graphTransformer = new Transformer<GraphMetadata, Graph<MyVertex, MyEdge>() {
    public Graph<MyVertex, MyEdge> transform(GraphMetadata metadata) {
        if (metadata.getEdgeDefault().equals(metadata.getEdgeDefault().DIRECTED)) {
            return new DirectedSparseGraph<MyVertex, MyEdge>();
        } else {
            return new UndirectedSparseGraph<MyVertex, MyEdge>();
        }
    }
};
{% endhighlight %}

This transformer is used to parse the `<graph>` tag in my GraphML file and create a new
`Graph` (it would really help if you had your GraphML file open at this point to understand
what the transformers are doing). This tag specifies the beginning of your graph, and whether
the graph is directed or undirected. The function `metadata.getEdgeDefault()` in this case
returns `"undirected"` which is equal to the library-defined constant
`metadata.getEdgeDefault().DIRECTED`. So this transformer checks whether the graph in the file
is directed and returns the required `Graph` object.

{% highlight java %}
/* Create the Vertex Transformer */
Transformer<NodeMetadata, MyVertex> vertexTransformer = new Transformer<NodeMetadata, MyVertex>() {
    public MyVertex transform(NodeMetadata metadata) {
        MyVertex v = MyVertexFactory.getInstance().create();
        v.setX(Double.parseDouble(metadata.getProperty("x")));
        v.setY(Double.parseDouble(metadata.getProperty("y")));
        return v;
    }
};
{% endhighlight %}

The vertex transformer is slightly more involved. I'll list out the various parts:

   * `MyVertexFactory`: This is my custom `Factory` that generates objects of my custom
     `MyVertex` class.
   * `MyVertexFactory.getInstance()`: This returns an object of the MyVertexFactory class
      that I can now use to access it's methods.
   * `v.setX(Double d)/v.setY(Double d)`: These are custom functions I've defined for my
     `MyVertex` class that set the `private int x` and `private int y` properties of the
      current vertex to the specified value.
   * `metadata.getProperty("x")`/`metadata.getProperty("y")`: This gets the value of the
      *x* and *y* properties that I've stored in my GraphML file (we used the `addVertexData`
      function in the previous post to save these out).

The vertex transformer parses the vertex data from the file and reads in its *x* and *y*
coordinates, and then sets these properties on the newly created `MyVertex` object.

{% highlight java %}
/* Create the Edge Transformer */
Transformer<EdgeMetadata, MyEdge> edgeTransformer = new Transformer<EdgeMetadata, MyEdge>() {
    public MyEdge transform(EdgeMetadata metadata) {
        MyEdge e = MyEdgeFactory.getInstance().create();
        return e;
    }
};
{% endhighlight %}

Similar to the previous transformer, this edge transformer reads in the edge data from the
file and creates a new edge. The `MyEdgeFactory` and `getInstance()` are analogous to those
just discussed for the `MyVertex` class.

{% highlight java %}
/* Create the Hyperedge Transformer */
Transformer<HyperEdgeMetadata, MyEdge> hyperEdgeTransformer = new Transformer<HyperEdgeMetadata, MyEdge>() {
    public MyEdge transform(HyperEdgeMetadata metadata) {
        MyEdge e = MyEdgeFactory.getInstance().create();
        return e;
    }
};
{% endhighlight %}

This is pretty much the same code as my edge transformer! My graphs didn't have hyper-edges,
but the GraphMLReader2 definition *requires* that you specify a hyperedge transformer too.

Finally, you create your graph reader object:

{% highlight java %}
/* Create the graphMLReader2 */
GraphMLReader2<Graph<MyVertex, MyEdge>, MyVertex, MyEdge> graphReader = new GraphMLReader2<Graph<MyVertex, MyEdge>, MyVertex, MyEdge>(fileReader, graphTransformer, vertexTransformer, edgeTransformer, hyperEdgeTransformer);
{% endhighlight %}

It's a pretty long statement to create one object, so make sure you've got all your angle brackets
in place.

{% highlight java %}
try {
    /* Get the new graph object from the GraphML file */
    Graph g = graphReader.readGraph();
} catch (GraphIOException ex) {}
{% endhighlight %}

Now you have your Graph object! Assuming you've worked with simple JUNG Graph objects enough to
want to save them out, you should be able to take it from here.

There is a small catch though; the graph right now will be displayed without any regard to the
`x` and `y` properties associated with its vertex objects. So you'll need to specify a
`StaticLayout` with a custom transformer, that reads in the x and y properties of each vertex
and places them accordingly on your canvas. You do that like this:

{% highlight java %}
StaticLayout<MyVerex, MyEdge> layout = new StaticLayout(g, new Transformer<MyVertex, Point2D>() {
    public Point2D transform(MyVertex v) {
        Point2D p = new Point2D.Double(v.getX(), v.getY());
        return p;
    }
});
{% endhighlight %}

This transformer is required to convert a vertex object to a `Point2D` object that the
layout needs to position its vertices. It creates a new `Point2D` object by using my custom
`getX()` and `getY()` methods that return the x and y properties of the vertex.
