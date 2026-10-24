---
title: "T-SQL Tuesday #50 - Automating Tasks"
date: "2014-01-14T07:00:53"
slug: "t-sql-tuesday-50-automating-tasks"
categories: ["SQL Server"]
tags: ["Automation", "SSIS"]
archived_comments: [{"author": "Glenda Gable", "date": "2014-01-14 15:23:12", "text": "Here is my post - great topic, thanks! :) http://sql313.com/index.php/menu-main-blog/14-maincat-dba/cat-automate/51-tsql-tuesdays-50"}]
---

[<img src="https://sqlchow.files.wordpress.com/2013/01/tsql2sday.png" class="alignleft" width="150" height="150" />](https://sqlchow.wordpress.com/2014/01/07/t-sql-tuesday-050-automation-how-much-of-it-is-the-same/)

This month's T-SQL Tuesday topic is the reason I love being a DBA, automating repetitive tasks.  Hemanth Damecharla ([b](http://sqlchow.wordpress.com)\|[t](https://twitter.com/sqlchow)) picked a timely topic, as you start the new year, are there certain tasks that you need to automate that tend to sit on the corner of your desk yelling at you?

This topic also reminds me of a chart I came across in the past describing the time savings associated with [automating repetitive tasks](http://chartporn.org/2012/05/10/repetitive-tasks/).  As at most places, we are all asked to do more with fewer resources.  This often leads to additional workloads without the time in the day to complete them.  How many of these can you automate?

<figure>
<a href="/wp-content/uploads/2014/01/yelling.jpg"><img src="/wp-content/uploads/2014/01/yelling.jpg" class="size-medium wp-image-631" width="300" height="199" alt="Automate some tasks!" /></a>
<figcaption>Automate some tasks!</figcaption>
</figure>

As I approach each task or even large projects, I like to start with a manual approach.  This gives me time to understand the business problem I'm solving and plan my attack for automation.  Some tasks don't need to be automated, they may be solved by using simple T-SQL statement can be built to solve the problem.  As soon as I run across tasks that contain multiple data sources, SSIS is my go to tool.  SSIS allows me to build modular packages that can be reused and organized for automation.

Back in 2012 when PASS was in Seattle, WA, I attend a pre-con for SSIS Design Patters hosted by Andy Leonard, Tim Mitchell, Matt Mason, Michelle Ufford, and Jessica Moss.  This really opened my mind to what's possible with SSIS.  I [recommend the book ](http://www.amazon.com/Server-Integration-Services-Design-Patterns/dp/1430237716/ref=sr_1_1?ie=UTF8&qid=1389371186&sr=8-1&keywords=ssis+design+patterns) that sparked the pre-con if you're interested in learning more.

As you start your automation effort, realize the upfront time spent may seem counter productive.  But the time invested now will pay benefits down the road.  Instead of having to manually run scripts (and having to be reminded to do so), your automated process will be running in the background making you look like a rock star!

Happy Automating
