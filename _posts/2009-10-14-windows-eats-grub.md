--- 
layout: post
title: Windows Eats Grub
tags: troubleshooting
---

This is a common problem that surfaces when you install a Windows OS after you install Ubuntu;
Windows conveniently wipes out the GRUB bootloader (the Linux equivalent of NTLDR, the
"Choose Operating System menu"), locking you out from booting into Ubuntu. The fix for this is
quick and easy in the typical case.

   * Boot from the live CD.
   * Mount your Linux partition; if you don't know which one that is, mount all your partitions. Do this by going to Places&gt;Computer and then double clicking on all the drives you see.
   * Open a terminal and follow the prompts on the grub console below:

{% highlight bash %}
sudo grub
grub> find /boot/grub/stage1
(hd0,5)
grub> root (hd0,5)
grub> setup (hd0)
grub> quit
{% endhighlight %}

That's it! Now just restart your computer, and don't forget to remove the CD from the drive!

Basically, what you're doing is asking grub to look for the file /boot/grub/stage1. This will
return the hard drive and partition number where your bootloader resides. In this case, my
bootloader is on the first hard drive, in the 6th partition. Numbering starts from 0! Then you
tell grub to set this as the root partition. And then you install the bootloader onto the MBR
of the first hard drive. This means that the grub isn't installed to a specific partition, but
to the Master Boot Record of the hard drive. It will wipe out any other bootloader you may have
installed there.
