--- 
layout: post
title: "pyFreeSMS: A Python API"
tags: python
---

This is a Python API to send free messages via the many online free SMS providers.
It currently works only with 160by2; I'll add support for Way2SMS et all soon, though
I'm hoping people interested in a specific provider will extend this API themselves.

## How Will This Help Me?

This is primarily intended for developers looking to send messages from their Python
applications. For instance, I'm currently developing an [application](http://passportbug.appspot.com) 
that periodically checks my passport application status and messages it to me.

## Getting It

   * Go [here](https://github.com/emaadmanzoor/pyFreeSMS/), click on the **Downloads**
     button at the top-right, and select the archive format that you're comfortable with.
   * Extracting the archive should now show you the `pyFreeSMS` folder and a `README` file.

## Using It

   * Copy the `pyFreeSMS` folder to the directory where your code resides.
   * Import the API:

{% highlight python %}
from pyFreeSMS import py160by2
{% endhighlight %}

   * Send your message with the `sendmessage(username, password, targetPhoneNumber, message)`
     function, replacing your account authentication details where necessary:

{% highlight python %}
py160by2.sendMessage('usrname','pwd','123','msg')
{% endhighlight %}

## Contributing

Considering the number of free SMS providers out there, I'm hoping there are a lot of you who
might want to extend this API to your liking. To start off, you'll first need to **install Git:**

{% highlight bash %}
sudo apt-get install git-core
{% endhighlight %}

Then you'll need to **get the code:**

{% highlight bash %}
git clone https://github.com/emaadmanzoor/pyFreeSMS.git
{% endhighlight %}

This will download the required source code to the current directory.
To commit your extended code and added modules, it'd be best to read up the
friendly documentation at [Github](https://github.com/) itself.
