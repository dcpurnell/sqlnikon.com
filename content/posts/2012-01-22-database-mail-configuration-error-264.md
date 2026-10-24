---
title: "Database Mail Configuration Error 264"
date: "2012-01-22T18:35:57"
slug: "database-mail-configuration-error-264"
categories: ["SQL Server"]
tags: ["2008", "Agent Job Notification", "Database Mail", "Error 264", "SQL Server Agent"]
---

As most of you know, the Database Mail feature in SQL Server 2008 is the life blood of any notification system for your instances.  If Database Mail fails to send notifications, you may not be warned if a job fails, or worst, a backup job.  We had a server last week that was exhibiting a weird behavior within Database Mail.  I was receiving mail from all parts of the Database Mail environment except for Agent Job Notifications.  I was able to send test emails from Database Mail, able to receive maintenance plan summary reports and even receive emails from within maintenance plans using the notification task.  Why was Agent Job Notifications the only area that was mis-behaving?  As I started diagnosing the issue I checked the main areas that usually stumped me in the past:

- Verified database mail profile was enabled under SQL Server agent (Alert System Page)
- Verified profile security was public and default
- Restarted SQL Server Agent

The above three items usually resolved any issue I have with Database Mail.  Did some more testing with my Agent Job and sure enough, still not working.  Then I started digging into the logs, under SQL Server 2008 you can see logs from SQL Server, SQL Server Agent, Database Mail, and Windows all under the same screen.  I dove into the Database Mail Log and there was an error for "\[264\] An attempt was made to send an email when no email session has been established".  Never seen this before.  I started searching Google and found similar issues but none seemed to fit my situation or solve my problem.  Because we have a simple setup for Database Mail, one account and one profile, I decided to rebuilt the configuration.

I deleted the profile and account, and then went back in and went through a complete rebuilt of the configuration.  I used the same account and same profile settings as before. After I had the Database Mail configuration complete, I needed to make sure the profile was enabled under SQL Server Agent.  Right click on SQL Server Agent and click Properties.  Under the Alert System page, make sure Enable Database Mail is enabled and that your mail system is selected along with the correct profile name.  With that done, I need to restart the SQL Server Agent.  Upon restart the 264 error did not appear and I was able to receive emails from my Agent Job Notifications.  Don't know what caused the issue in the first place, but the rebuild seemed to clear things up.
