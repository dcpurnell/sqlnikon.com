---
title: "Virtual Book Club: SQL Server Execution Plans, Chapter 2"
date: "2013-09-17T07:52:51"
slug: "virtual-book-club-sql-server-execution-plans-chapter-2"
categories: ["SQL Server"]
tags: ["Book Review", "Query Optimizer", "Query Plan"]
---

[<img src="/wp-content/uploads/2013/09/sql-server-execution-plans.jpg" class="alignright size-medium wp-image-185" width="243" height="300" alt="SQL Server Execution Plans" />](/wp-content/uploads/2013/09/sql-server-execution-plans.jpg)

Everyone loves reading a good book, especially about SQL Server.  I've been on a training kick lately and the timing of this book club was perfect.  Denis Gobo ([b](http://denis-gobo.squarespace.com/)\|[t](https://twitter.com/DenisGobo)) has experience starting a book club where he works and decided to bring it to the SQL Server community.  The goal of the club is to read a chapter each week and discuss things you learned, liked and disliked.  You can ready Denis's original post [here](http://denis-gobo.squarespace.com/denisgobo/2013/9/3/virtual-book-club-who-is-in).  The first book chosen was written by Grant Fritchey ([b](http://www.scarydba.com/)\|[t](https://twitter.com/gfritchey)) and is titled "SQL Server Execution Plans, Second Edition".  You can get a free electronic copy or purchase a print copy from [simple-talk.com](https://www.simple-talk.com/books/sql-books/sql-server-execution-plans,-second-edition,-by-grant-fritchey/).

Continuing with my [review of Chapter 1](/2013/09/05/virtual-book-club-sql-server-execution-plans-chapter-1/), here are my thoughts on Chapter 2.  You could think of Chapter 1 as walking into the shallow end of the pool and Chapter 2, swimming into the deep end, but in a good way.  I never felt like I was drowning in the material, all the topics were presented in a way that made it easy to comprehend.

## Things I learned

Blocking/Non-Blocking determines when an operator can begin processing data.  Blocking operators need to wait for all the data before they can begin outputting data (Hash-Join is an example of a blocking operation).  Non-Blocking, on the other hand, can begin processing as soon as the data starts arriving (Merge-Join is an example of a non-blocking operation).  This subtle idea can help you better understand how data flows between your operators.

Sorting is something I always used as a presentation technique but in the world of query plans and table joins it can have a big impact on the optimizer's plan generation.  For example, a merger-join will only be used on sorted data, period.  But if you have two non-sorted lists, hash-join may be a better option.  Because hash-joins builds temporary table with in tempdb, too many of them can cause tempdb performance issues.

Depending on the data sets, hash-join may be a good fit (think small data sets).  They should also be warning sign.  Pay attention to missing indexes, a missing WHERE clause, or calculations in the WHERE clause that can make it non-[sargable](http://stackoverflow.com/questions/799584/what-makes-a-sql-statement-sargable) (unable to use an index).

When using SET STATISTICS IO ON to better understand logical and physical page reads, scan count was something that I was aware of but didn't fully understand.  There is a great [blog post](http://blogs.msdn.com/b/sqlserverfaq/archive/2010/09/14/scan-count-meaning-in-set-statistics-io-output.aspx) on MSDN that explains when you will see scan count 0, 1 or N.  Just think of it as how many times a scan is started looking for data in a data set.

When generating a query plan for an UPDATE statement, the optimizer has to first determine what rows need to be updated.  This is accomplished by first doing scan/seek operation.  Pay attention to the WHERE clause of your UPDATE statement as this will determine how efficient the select portion of the UPDATE statement will be.

## Likes

Even though there was plenty more information presented in chapter 2 over chapter 1, everything was clear and concise.  Following along with the scripts on my local instance of SQL Server made the query plans easier to follow and I was spend more time understanding how the optimizer behaves.

## Dislikes

There were only a few things that I would have liked to see presented better.  Under the Nested Loops Join section, the tool top defines it as "For each row in the top (outer) input, scan the bottom (inner) input, and output matching rows.  But Grant explained it as "... scanning the outer data set (the bottom operator in a graphical execution plan) once for each row in the inner set".  Grants explanation seemed on contradict the tool tip so I had to spend extra time reading through this section to understand what was actually happening within the nested loops join.

Scan count was referenced under the Filtering Data section but no time was given to explain if a low/high scan count was a sign of possible problems.  But, as I do with other blog posts, when I hit a term and I don't understand I search for it.  I was able to find a [blog post](http://blogs.msdn.com/b/sqlserverfaq/archive/2010/09/14/scan-count-meaning-in-set-statistics-io-output.aspx) under MSDN that did a great job of explaining how it works as well as samples to show what would cause 0, 1, and N scan counts.

On to chapter 3!
