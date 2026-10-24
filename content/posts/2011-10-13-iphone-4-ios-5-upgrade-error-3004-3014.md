---
title: "iPhone 4 IOS 5 Upgrade Error 3004 & 3014"
date: "2011-10-13T09:31:01"
slug: "iphone-4-ios-5-upgrade-error-3004-3014"
categories: ["Apple"]
tags: ["error", "iOS 5", "iPhone 4", "iTunes", "update", "upgrade"]
---

I was excited to see the iOS 5 update was available yesterday (10/12/11) so I did what any normal person would do and quickly connected my iPhone 4 via iTunes and clicked the Check for Update button.  The download was about 740MB and didn't take too long to pull down from Apple's site.  The install appeared to be going well until it started the restore process and bombed out with an error code 3004/3014.  Did some research via Google and didn't find an exact fix but found plenty of other people experiencing the same problem.  I was able to get past the verification stage with Apple, but the restore was failing every time I tried update the phone.  I was stuck in an infinite loop.  The phone would have the factory default "Connect to iTunes" message, but every time it went to restore the iOS 5 image it failed.  I finally ran across a few articles taking about pulling the iOS 5 image down directory from Apple and applying that image instead of the one that was pulled down from iTunes.  You can find the iOS 5 image links to all the Apple devices compatible with iOS 5 [here](http://techie-buzz.com/mobile-news/ios5-ipsw-direct-download-links.html).

Once I had the iPhone3,1_5.0_9A334_Restore.ipsw file (specific to my at&t iPhone 4) I connected the phone back to the USB cable and this time, held down the Option key and clicked Restore within iTunes under my device.  This brought up a finder window that enabled me to select my own iOS 5 image to use.  This restored the phone to the original factory defaults (with iOS 5) and got my phone back up and running.  Once iTunes discovered the same phone had been previously backed up on the same machine, it let me select the backup image to apply.  This process took a while.  All the settings, apps, music, and videos had to be copied back to the iPhone.  Once that completed (~1.5 hours) I was back in shape!

I miss Steve...
