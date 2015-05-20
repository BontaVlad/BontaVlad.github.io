--- 
layout: post
title: Getting Android Sources Behind A Restrictive Proxy
tags: android
---

I'll have to assume you're suffocated by both the following bottlenecks in getting the Android
Open Source Project code:
 
   * Blocked `git://` protocol and port.
   * A limit on the amount you're allowed to download.

The Android sources amount to around 6GB in total, so anonymous proxy programs like
[Your-Freedom](http://www.your-freedom.net/) will choke after a fixed time limit;
and `repo sync` (git) does not resume downloads between projects; though you may resume
from the last project you downloaded. To smoothen out the rough edges, do this:

   * Set your git proxy using this command, replacing what's necessary:
     `git config --global http.proxy 10.1.8.30:8080`
   * Follow the steps [here](http://source.android.com/source/download.html) until you reach
     *Getting The Files*: this is the part that won't work behind a restrictive proxy.
   * Switch to the directory where you initially ran `repo init -u` on the command line and
     then type in `ls -a`; you should be able to see a `.repo` folder. If you don't, it means
     your `repo init -u` failed for some reason.
   * Type in `gedit .repo/manifest.xml` and change line 4 to read:
     `fetch="https://android.git.kernel.org/`
   * Type in `gedit .repo/repo/repo` and change line 5 to read:
     `REPO_URL='http://android.git.kernel.org/tools/repo.git'`
   * Download the modified repo script
     [here](https://docs.google.com/leaf?id=0B76d_EyUt5JwNDU5NzFiNzMtYWQ1NC00ZmNlLThiNjQtY2M1NTM3MDQzMzBi&amp;hl=en)
     and replace your old repo script with the modified one.
   * Continue with *Getting The Files* at the
     [Android Open Source Project website](http://source.android.com/source/download.html)
     and things should be working fine.
