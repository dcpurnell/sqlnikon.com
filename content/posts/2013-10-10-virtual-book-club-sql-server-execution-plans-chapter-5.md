---
title: "Virtual Book Club: SQL Server Execution Plans, Chapter 5"
date: "2013-10-10T07:11:01"
slug: "virtual-book-club-sql-server-execution-plans-chapter-5"
categories: ["SQL Server"]
tags: ["Book Review", "Query Optimizer", "Query Plan"]
---

[<img src="/wp-content/uploads/2013/09/sql-server-execution-plans.jpg" class="alignright size-medium wp-image-185" width="243" height="300" alt="SQL Server Execution Plans" />](/wp-content/uploads/2013/09/sql-server-execution-plans.jpg)

Everyone loves reading a good book, especially about SQL Server.  I've been on a training kick lately and the timing of this book club was perfect.  Denis Gobo ([b](http://denis-gobo.squarespace.com/)\|[t](https://twitter.com/DenisGobo)) has experience starting a book club where he works and decided to bring it to the SQL Server community.  The goal of the club is to read a chapter each week and discuss things you learned, liked and disliked.  You can ready Denis's original post [here](http://denis-gobo.squarespace.com/denisgobo/2013/9/3/virtual-book-club-who-is-in).  The first book chosen was written by Grant Fritchey ([b](http://www.scarydba.com/)\|[t](https://twitter.com/gfritchey)) and is titled "SQL Server Execution Plans, Second Edition".  You can get a free electronic copy or purchase a print copy from [simple-talk.com](https://www.simple-talk.com/books/sql-books/sql-server-execution-plans,-second-edition,-by-grant-fritchey/).

Continuing with my [review of Chapter 4](/2013/10/01/virtual-book-club-sql-server-execution-plans-chapter-4/), here are my thoughts on Chapter 5.  The optimizer is very good at what it does,  but no one is perfect.  There may be rare cases where the optimizer needs a hint to force a certain type of behavior.  Although this may bring immediate gains in query performance, over time, the new plan generated may cease to function better than the what the optimizer can compile on the fly.  The reason for this is data change.  As the data changes, statistics are updated and the selectivity of the data changes which causes indexes to become more or less useful.  This is why using hints is dangerous and should be used sparingly.

## Things I learned

Besides using the occasional evil hint 'WITH (NO LOCK)', I don't use hints.  Partly because I didn't understand the query plans that well before reading this book and I had lots of respect for the optimizer.  Now that I understand how execution plans are generated, I can see a useful need for hints, testing.  To be able to change the behavior of the optimizer by using a Query, Join or Table hint is a powerful learning tool.  You can start from the optimizer's auto generated plan and start poking it with hints to see how the I/O and query time changs.

If I were to start using hints, I would definitely see a need for a tracking document or metadata query to reevaluate the execution plans.  If the tables involved are static in nature, you may not need to bother with reworking the query plan hints but once a year.  On the flip side though, a monthly review may be necessary if the query is pulling data from volatile tables.

## Likes

Even though controlling execution plans with hints is frowned upon, Grant did a great job going through examples of each hint and how you can use them to better understand the optimizer.  Grant may it very clear throughout the chapter to use hints at your own risk, but if you find a select operator has timed out looking for the best plan you may have an opportunity to use hints.

## Dislikes

As with most chapters thus far, no complaints on the material presented.

On to chapter 6!
