--- 
layout: post
title: "Quick Fix: Natty, Ubuntu Classic and Compiz"
tags: compiz ubuntu
---

If you're reading this, you must be a Unity reject: the ones who upgraded to Natty and are
now left in the cold after being told their hardware's just too yesterday. If you're beginning
to miss your wobbly windows and other frills on Ubuntu Classic, give this quick hack a try.

### Get rid of `unity-window-decorator`

{% highlight bash %}
sudo killall unity-window-decorator
{% endhighlight %}

If you get a message saying `unity-window-decorator: no process found`, it means the
decorator isn't running, move on.

### Get back `gtk-window-decorator`

   * Start **CompizConfig Settings Manager**: `ccsm`
   * Open up the **Window Decoration** settings
   * Change **Command** to: `gtk-window-decorator --replace`
   * **Close** CompizConfig Settings Manager

You can configure your old frills and see them in action now. All that's left is making sure
everything remains frilly after the next reboot:

### Set up `fusion-icon`:

  * **Install:** `sudo apt-get install fusion-icon`
  * **Start:** `fusion-icon`

You'll see a cool icon in your notification area; right click on it and ensure the
**Select Window Manager** setting is **Compiz** and the **Select Window Decorator**
setting is **GTK Window Decorator**.

### Set `fusion-icon` as a startup application:

System --> Preferences --> Startup Applications --> Add; then enter the values:

  * **Name:** fusion
  * **Command:** `fusion-icon --sleep 5`
  * **Comment:** Start fusion-icon with a delay of 5 seconds after startup

Test the setup on the next reboot: you'll notice a slight flash in the first few seconds;
this is fusion-icon starting the Compiz window manager, pretend you didn't notice. I guess
this quick fix should hold up until we get some real ones from the Compiz/Unity guys.
