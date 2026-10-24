---
title: "T-SQL Tuesday #101 - Essential SQL Server Tools"
date: "2018-04-10T17:17:17"
slug: "t-sql-tuesday-101-essential-sql-server-tools"
categories: ["SQL Server"]
---

[<img src="/wp-content/uploads/2017/12/sqltuesday.png" class="alignleft wp-image-662 size-full" width="129" height="130" />](http://t-sql.dk/?p=1947)This month’s \#tsql2sday is being hosted by Jens Vestergaard ([b](http://t-sql.dk)\|[t](https://twitter.com/vestergaardj)). His topic is about the [essential SQL Server tools in my stack](http://t-sql.dk/?p=1947). I’m looking forward to reading the summary post to find out what tools I’m missing out on.

One of the foundation tools we put on all our instances is [Ola Hallengrens’s maintenance scripts](https://ola.hallengren.com). It makes backups, indexes, and integrity checks very easy. This is hands down a much better tool to use over the built-in Maintenance Plans under SSMS.

<figure>
<img src="/wp-content/uploads/2014/01/yelling-300x199.jpg" class="size-medium wp-image-631" width="300" height="199" />
<figcaption>Restore the database now!</figcaption>
</figure>

One of the best practices around backups is having restore scripts within arms reach. This functionality is not built into Ola’s solution but Jared Zagelbaum ([b](https://jaredzagelbaum.wordpress.com)\|[t](https://twitter.com/jaredzagelbaum)) has written an extension\
that handles this for you. The idea is when the call comes in a 3:00 am about corruption or another reason that requires a restore, you have the scripts ready without having to slap your brain out of a sleeping fog.

Jared’s extension works by adding an additional step to Ola’s backups jobs to create and text file with restore statements for all database with the latest full, diff, and/or transaction log backup files in the backup chain.

You can find his blog post that talks about his solution [here](https://jaredzagelbaum.wordpress.com/2015/04/16/automated-restore-script-output-for-ola-hallengrens-maintenance-solution/) and a link the GitHub files [here](https://github.com/jzagelbaum/OlaHallengrenRestoreScript). Thanks to Jared for sharing and allowing me to sleep better at night.
