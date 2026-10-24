---
title: "F11 and VMware ESXi 5 on my Mac"
date: "2011-10-04T14:20:36"
slug: "f11-and-vmware-esxi-5-on-my-mac"
categories: ["Apple"]
tags: ["ESX", "iDRAC", "lab", "Mac", "Mission Control", "System Preferences"]
---

As I was installing ESXi v5 in my lab I came across a prompt to press F11 to accept the license agreement, that I fully read :).  On my Mac I was using iDRAC v6 Enterprise via the browser to install the ISO image.  When I went to press F11, my Mac's desktop was shown.  I have the full Apple USB keyboard so I tried using the fn key with F11 and without, each time with no success.  I thought I'd start in the System Preferences section under Keyboard.  Under the Mission Control section there was a short-cut for F11 and F12 that was grabbing the keystroke before it was sent through the browser.

[<img src="/wp-content/uploads/2011/10/screen-shot-2011-10-04-at-2-10-34-pm1.png" title="Keyboard Options for Mission Control" class="alignnone size-full wp-image-54" width="500" height="447" />](/wp-content/uploads/2011/10/screen-shot-2011-10-04-at-2-10-34-pm1.png)

Once I un-checked the "Show Desktop" and "Show Dashboard" I was able to reply to the license agreement prompt with F11.
