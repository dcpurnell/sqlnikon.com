---
title: "Virtual Book Club: SQL Server Execution Plans, Chapter 1"
date: "2013-09-05T14:11:09"
slug: "virtual-book-club-sql-server-execution-plans-chapter-1"
categories: ["SQL Server"]
tags: ["Book Review", "Query Optimizer", "Query Plan"]
---

[<img src="/wp-content/uploads/2013/09/sql-server-execution-plans.jpg" class="alignright size-medium wp-image-185" width="243" height="300" alt="SQL Server Execution Plans" />](/wp-content/uploads/2013/09/sql-server-execution-plans.jpg)

Everyone loves reading a good book, especially about SQL Server.  I've been on a training kick lately and the timing of this book club was perfect.  Denis Gobo ([b](http://denis-gobo.squarespace.com/)\|[t](https://twitter.com/DenisGobo)) has experience starting a book club where he works and decided to bring it to the SQL Server community.  The goal of the club is to read a chapter each week and discuss things you learned, liked and disliked.  You can ready Denis's original post [here](http://blogs.lessthandot.com/index.php/DataMgmt/DBAdmin/MSSQLServerAdmin/virtual-book-club-who-is).  The first book chosen was written by Grant Fritchey ([b](http://www.scarydba.com/)\|[t](https://twitter.com/gfritchey)) and is titled "SQL Server Execution Plans, Second Edition".  You can get a free electronic copy or purchase a print copy from [simple-talk.com](https://www.simple-talk.com/books/sql-books/sql-server-execution-plans,-second-edition,-by-grant-fritchey/).

This is actually my first book review.  Following Denis's lead, I'm going to discuss what things I learned, what I liked about the chapter and areas I disliked.  As with speakers, feedback is important for authors.  Hopefully our discussion of the book will help Grant on his third edition.

## Things I learned

Did you know that you can save a XML version of the execution plan and share them with others?  Well, neither did I.  This would be a great way to get feedback on better ways to build queries.  In fact [SQLPerformance.com](http://www.sqlperformance.com/2013/02/t-sql-queries/plan-explorer-upload-feature) offers the ability to upload your plan directly from SQL Sentry's [Plan Explorer](http://www.sqlsentry.net/plan-explorer/sql-server-query-view.asp) to their Q&A site.  The SQL Server community has a wealth of information and there are always folks available to help you with your questions.

I'm a big fan of Idera's SQL [Diagnostic Manager](http://www.idera.com/productssolutions/sqlserver/sqldiagnosticmanager).  This tool makes it easy to see trouble areas within my SQL Server instances.  The only down side is that I'm not using the DMO statements on a daily basis.  With DMOs you're able to pull a specific plan from the plan cache.  This is useful when you're developing queries and need to view a plan that may have been saved from a previous execution of your query.  To interact with some DMOs, you need to use the APPLY operator because the DMOs are table-valued functions.  I've known about APPLY but have not had the need to use it in my daily work.

## Likes

Grant did a great job introducing the query engine and how a plan is ultimately built and saved for later use.  Having a strong understanding of how the execution plan is built will help me write better queries.  Grant didn't throw too much material at me during the first chapter.  This allowed me to comprehend the material better without feeling overwhelmed.

## Dislikes

I didn't find anything in this chapter that came across as a dislike and I'm guessing this trend will continue for the remainder of the book.

I'm looking forward the chapter 2 next week and the rest of the book.  My goal is to be able to read execution plans better than seeing how thick the lines are between operators.
