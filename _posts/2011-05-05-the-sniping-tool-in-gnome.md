--- 
layout: post
title: The Sniping Tool in Gnome
tags: gnome ubuntu
---

For the uninitiated, it's a nifty tool I've seen being used on Vista that lets you select an area of the screen to take a screenshot of, instead of the entire screen; and it's been lying around on Gnome all this while!

To try it out:

   * System --> Preferences --> Keyboard Shortcuts --> **Add**
      * **Name:** Snipe
      * **Command:** gnome-screenshot -ai
   * **Apply**; then click on your new entry to configure a shortcut key

This binds your shortcut-key to the Gnome Screenshot tool, being started in the `-a(rea)`
and `-i(nteractive)` mode. If you prefer seeing the sniping crosshairs directly instead
of an interactive dialog, use `gnome-screenshot -a` as the command instead.
