--- 
layout: post
title: "Verilog On Linux: Defenestrating Modelsim"
tags: verilog
---

> Defenestrate */diˈfɛnəˌstreɪt/* (verb) : to throw (a person or thing) out of a window.
> The word originated from a couple of incidents in Prague, back in the 14th century, when
> a bunch of guys stormed in and tossed seven town officials out the window (quite literally).

This tutorial's to the victims of the Modelsim user experience, forced to design hardware in
chains and gracefully handle the precious rear end of the popular musty racehorse that's
Mentor Graphics' stable-star. If you're on Linux, freedom's a nice option.

I'll walk you through the steps to start coding in Verilog on your Linux box:

## Install the simulator and graphing tools

We use the [Icarus Verilog Simulator](http://www.icarus.com/eda/verilog/)
and [GTKWave](http://en.wikipedia.org/wiki/GTKWave).

{% highlight console %}
sudo apt-get install verilog gtkwave
{% endhighlight %}

## Code

Save the following code out into two files: `counter.v` and `counter_tb.v`. 

{% highlight verilog %}
// counter.v
module counter(out, clk, reset);

  parameter WIDTH = 8;

  output [WIDTH-1 : 0] out;
  input            clk, reset;

  reg [WIDTH-1 : 0]   out;
  wire            clk, reset;

  always @(posedge clk)
    out &lt;= out + 1;

  always @reset
    if (reset)
      assign out = 0;
    else
      deassign out;

endmodule // counter

// counter_tb.v
module test;

 /* Make a reset that pulses once. */
 reg reset = 0;
 initial begin
 $dumpfile(&quot;test.vcd&quot;);
 $dumpvars(0,test);

 # 17 reset = 1;
 # 11 reset = 0;
 # 29 reset = 1;
 # 5  reset =0;
 # 513 $finish;
 end

 /* Make a regular pulsing clock. */
 reg clk = 0;
 always #1 clk = !clk;

 wire [7:0] value;
 counter c1 (value, clk, reset);

 initial
 $monitor(&quot;At time %t, value = %h (%0d)&quot;,
 $time, value, value);

endmodule // test
{% endhighlight %}

## Compile and run the code

Open a terminal in the same directory and compile the code with this command:

{% highlight console %}
iverilog -o dsn counter_tb.v counter.v
{% endhighlight %}

Run the code with this command: `vvp dsn`

Simulate the generated output with this: `gtkwave test.vcd &`

Expand `test` on the top-left panel and select `c1`, then drag the signals from the
bottom-left (wire, reg) to the Signals panel to it's immediate right. This should get
you out on the right side of the bed with Verilog on Linux. Your next steps lie
[here](http://iverilog.wikia.com). All sample code and instructions are merely distilled
from the extensive documentation at the wiki linked to above. 
