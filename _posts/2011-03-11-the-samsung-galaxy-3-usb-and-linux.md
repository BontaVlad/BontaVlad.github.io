--- 
layout: post
title: The Samsung Galaxy 3, Android, USB and Linux
tags: android
---

This is a hack to get the Samsung Galaxy 3 to mount as a USB drive on Linux. For some reason,
it doesn't react to being plugged in to my computer, apart from a meek beep and an indication
that it's slyly sucking power from the USB port.

   * Disconnect your phone from the computer.
   * Settings --> About Phone --> USB Settings --> **Ask on connection**
   * Settings --> Applications --> Development: Check both **USB debugging** and
     **Stay awake**.
   * Dial `*#7284#` to open **PhoneUtils**.
   * Set both the UART and USB modes to **PDA** instead of Modem.
   * Connect the phone to the computer.
   * You should now receive some sort of USB notification on your phone;
     you know what to do from here.

This worked for me! Do post in your comments if it worked for you too, or not.

*You may need to change the PhoneUtils settings back to the old ones when using your phone as
a USB modem.*
