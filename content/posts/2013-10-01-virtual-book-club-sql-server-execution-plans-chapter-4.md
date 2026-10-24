---
title: "Virtual Book Club: SQL Server Execution Plans, Chapter 4"
date: "2013-10-01T07:34:38"
slug: "virtual-book-club-sql-server-execution-plans-chapter-4"
categories: ["SQL Server"]
tags: ["Book Review", "Query Optimizer", "Query Plan"]
---

[<img src="/wp-content/uploads/2013/09/sql-server-execution-plans.jpg" class="alignright size-medium wp-image-185" width="243" height="300" alt="SQL Server Execution Plans" />](/wp-content/uploads/2013/09/sql-server-execution-plans.jpg)

Everyone loves reading a good book, especially about SQL Server.  I've been on a training kick lately and the timing of this book club was perfect.  Denis Gobo ([b](http://denis-gobo.squarespace.com/)\|[t](https://twitter.com/DenisGobo)) has experience starting a book club where he works and decided to bring it to the SQL Server community.  The goal of the club is to read a chapter each week and discuss things you learned, liked and disliked.  You can ready Denis's original post [here](http://denis-gobo.squarespace.com/denisgobo/2013/9/3/virtual-book-club-who-is-in).  The first book chosen was written by Grant Fritchey ([b](http://www.scarydba.com/)\|[t](https://twitter.com/gfritchey)) and is titled "SQL Server Execution Plans, Second Edition".  You can get a free electronic copy or purchase a print copy from [simple-talk.com](https://www.simple-talk.com/books/sql-books/sql-server-execution-plans,-second-edition,-by-grant-fritchey/).

Continuing with my [review of Chapter 3](/2013/09/19/virtual-book-club-sql-server-execution-plans-chapter-3/), here are my thoughts on Chapter 4.  This chapter was a deeper dive into some of the more complex plans that can be generated from T-SQL statements like APPLY, CTEs, MERGE, views, as well as how indexes are chosen.

## Things I learned

Writing queries is an art form, you need to understand all the T-SQL statements and how they affect the query plan.  Don't get stuck on always using one technique over another.  For example, adding a WHERE clause to a sub-select may out perform an APPLY statement (based on the data set).  The point here is by understanding how each T-SQL statement will interact with your data, you can try different approaches to solving your problem and reach the results in the most efficient way.

Using ROLLBACK can be a useful approach when needing to view the actual execution plan for UPDATE, INSERT, DELETE, or MERGE statements.  This allows the actual query plan to be generated but the DML is not committed to the database allowing you to repeatedly change the query to generate the best quality plan.

## Likes

Grant did a great job of teaching how to dissect large query plans.  Just like when you are trying to each an elephant, you need to approach large query plans one operator at a time.  I also thought the way Grant explained views and indexes was very thorough.  I now have a better understand of when a view might be expanded to the table level or when an index might be passed over because of bad statistics.

The other thing I noticed is how Grant was able to sharpen our understanding of T-SQL and database fundamentals in the process of this chapter.  Being able to learn how the query optimizer generates plans while learning better uses of sub-queries, APPLY, CTEs, MERGE, views, and indexes is a great thing.

## Dislikes

As with most chapters thus far, no complaints on the material presented.  Just a minor typo on the T-SQL Listing 4.7.  The parameter being passed to the SP should be @BusinessEntityID and not @EmployeeID.

On to chapter 5!
