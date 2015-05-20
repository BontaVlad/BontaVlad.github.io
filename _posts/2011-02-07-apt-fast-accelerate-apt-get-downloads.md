--- 
layout: post
title: "apt-fast: Accelerate Apt-Get Downloads"
tags: linux
---

apt-fast accelerates your apt-get downloads using axel as a download manager.
Axel segments the downloads and fetches them from multiple servers; typical download manager
stuff. The developer claims an increase in speed of up to **26 times**.

## Install apt-fast

   * Add `ppa:tldm217/tahutek.net` to your Software Repositories
   * `sudo apt-get update`
   * `sudo apt-get install apt-fast`

## Configure Your Proxy

   * `sudo gedit /etc/axelrc`
   * Look for the line `# http_proxy =` and change this to `http_proxy = http://10.1.8.30:8080`.
     Ensure you remove the leading `#` and replace `10.1.8.30:8080` with your own proxy host
     and port.
   * Save and close gedit

## Try it out

{% highlight bash %}
sudo apt-fast update
sudo apt-fast upgrade
sudo apt-fast install your-package
{% endhighlight %}
