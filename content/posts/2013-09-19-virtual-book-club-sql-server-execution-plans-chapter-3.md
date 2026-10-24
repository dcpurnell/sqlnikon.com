---
title: "Virtual Book Club: SQL Server Execution Plans, Chapter 3"
date: "2013-09-19T07:40:29"
slug: "virtual-book-club-sql-server-execution-plans-chapter-3"
categories: ["SQL Server"]
tags: ["Book Review", "Query Optimizer", "Query Plan"]
---

[<img src="/wp-content/uploads/2013/09/sql-server-execution-plans.jpg" class="alignright size-medium wp-image-185" width="243" height="300" alt="SQL Server Execution Plans" />](/wp-content/uploads/2013/09/sql-server-execution-plans.jpg)

Everyone loves reading a good book, especially about SQL Server.  I've been on a training kick lately and the timing of this book club was perfect.  Denis Gobo ([b](http://denis-gobo.squarespace.com/)\|[t](https://twitter.com/DenisGobo)) has experience starting a book club where he works and decided to bring it to the SQL Server community.  The goal of the club is to read a chapter each week and discuss things you learned, liked and disliked.  You can ready Denis's original post [here](http://denis-gobo.squarespace.com/denisgobo/2013/9/3/virtual-book-club-who-is-in).  The first book chosen was written by Grant Fritchey ([b](http://www.scarydba.com/)\|[t](https://twitter.com/gfritchey)) and is titled "SQL Server Execution Plans, Second Edition".  You can get a free electronic copy or purchase a print copy from [simple-talk.com](https://www.simple-talk.com/books/sql-books/sql-server-execution-plans,-second-edition,-by-grant-fritchey/).

Continuing with my [review of Chapter 2](/2013/09/17/virtual-book-club-sql-server-execution-plans-chapter-2/), here are my thoughts on Chapter 3.  This chapter was short and sweet.  XML plans were the main focus and this chapter gave me some great ideas on how to use XQuery to make reading the XML based plans easier.

## Things I learned

I've always stayed away from XML.  In my many years working in the database world I have not had the need to interact with XML data.  Querying XML based query plans with XQuery is first time I've seen a benefit of using XML as a DBA.  For larger plans it will be easier to query the XML data instead of trying to hunt down operations with in the graphical view.

You can use XQuery to query .sqlplan files, XML data stored in columns or directly from the plan cache.  Caution needs to be used when querying directly against the plan cache as this can have performance side effects.

## Likes

I liked how Grant told us upfront in the first part of chapter that if you're not dealing with SQL Server instances before version 2005 that text-based query plans may not be something you need to understand.  Besides being a deprecated feature, XML offers plenty of advantages over text-based plans.

## Dislikes

Nothing to dislike in this chapter.  There was just a minor typo in the supplied script for chapter 3.  The book references Listing 3.18 but in the script file it is listed as 3.19

On to chapter 4!
