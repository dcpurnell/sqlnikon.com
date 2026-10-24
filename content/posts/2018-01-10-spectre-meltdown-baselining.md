---
title: "Spectre/Meltdown Baselining"
date: "2018-01-10T11:25:55"
slug: "spectre-meltdown-baselining"
categories: ["SQL Server"]
tags: ["tsql2sday", "baseline", "Meltdown", "Power BI", "sp_BliztFirst", "Spectre"]
archived_comments: [{"author": "Brent Ozar", "date": "2018-01-10 11:27:53", "text": "Awesome, glad we could help! That's exactly the way I use those tools myself, too."}, {"author": "Andrew Tobin", "date": "2018-01-10 12:21:44", "text": "Nice! I'm starting at a new place on Monday with some perf (CPU) problems and I'm going to walk in and be asked about Spectre/Meltdown I bet. I'll probably be doing something similar to see if we can patch early, or if we need to fix some issues to give us some breathing room first.\n\nThanks for posting the advice :)"}]
---

[<img src="/wp-content/uploads/2014/01/t-sql-tuesday.png" class="alignleft wp-image-630 size-full" width="150" height="150" />](https://blobeater.blog/2018/01/02/t-sql-tuesday-98-your-technical-challenges-conquered/)This month’s \#tsql2sday is being hosted by Arun Sirpal ([b](https://blobeater.blog)\|[t](https://twitter.com/blobeater1)). The topic this month is how we conquered a technical challenge. The area I’ve been spending the most time in recently is baselining for the Spectre/Meltdown patches that are coming. We have a monitoring tool from [Idera](https://www.idera.com/productssolutions/sqlserver/sqldiagnosticmanager), SQL Diagnostic Manager, on our key production boxes but I wanted something consistent across all boxes that we could use for tracking and baselining wait types.

<img src="/wp-content/uploads/2018/01/meltdown-spectre-100745817-large-300x218.jpg" class="size-medium wp-image-733 aligncenter" width="300" height="218" />The Spectre/Meltdown can have a significant [performance impact](https://cloudblogs.microsoft.com/microsoftsecure/2018/01/09/understanding-the-performance-impact-of-spectre-and-meltdown-mitigations-on-windows-systems) on servers running Windows Server OS that have intensive IO-intensive applications. SQL Server falls right into this area. We need a way to identify CPU changes across all our instances (dev/test/prod) while we apply the patches

There are plenty of queries to help identify wait types but I was looking for something that could be put into place quickly as patches from VMware and Microsoft are being released this week. I found the perfect one, [sp_BlitzFirst](https://www.brentozar.com/askbrent/) from Brent Ozar Unlimited.

Their solution gives you the wait stat breakdown and reporting to help you identify baseline changes. When you have limited time to put something in place, these types of solutions from community partners are a great place to start. Having baseline wait stats has been on my list for years. There was always another project that was pushed to the front of the list, but now Spectre/Meltdown is at the top of my list!

I used the following [blog post](https://www.brentozar.com/first-aid/first-responder-kit-power-bi-dashboard/) to get me started. We have all of our instance registered and organized under a [Central Management Server](https://docs.microsoft.com/en-us/sql/ssms/register-servers/create-a-central-management-server-and-server-group). This feature allows us to run a query across multiple instances at once. I pulled down the latest [First Responder Kit](https://www.brentozar.com/first-aid/) which includes the script to schedule and a Power BI report to analyze the results.

The next phase was how to identify a process to baseline. We don’t have any automated tools to regression test our apps (something else to work on) so I needed something to stress our SQL Server instances and record the wait types throughout the patching process. Once again the fine folks at Brent Ozar Unlimited had a [blog post](https://www.brentozar.com/archive/2015/05/how-to-fake-load-tests-with-sqlquerystress/) for this problem as well. Using [SQLQueryStress](https://github.com/ErikEJ/SqlQueryStress), we can simulate a load on our SQL Server Instances and record the wait types. After each patch, we can execute the same load and compare the results using Power BI.

When faced with a technical challenge like Spectre/Meltdown, having a process in place to baseline your SQL Server Instances is important to show how changes to your environment can have lasting effects on performance.
