---
title: "T-SQL Tuesday #112 Cookie Monster"
date: "2019-03-12T20:24:34"
slug: "t-sql-tuesday-112-cookie-monster"
categories: ["SQL Server"]
---

<figure class="alignleft">
<figure>
<a href="https://nocolumnname.blog/2019/03/05/t-sql-tuesday-112-dipping-into-your-cookie-jar/"><img src="/wp-content/uploads/2017/12/sqltuesday.png" class="wp-image-662" /></a>
</figure>
</figure>

Shane O’Neill ([b](https://nocolumnname.blog)\|[t](https://twitter.com/SOZDBA)) is hosting this month’s edition of \#TSQL2sDay. Shane’s charged to us is to think back when we had a difficult time with project/task and used our internal mojo (cookie jar) for energy to keep going.

\
We have custom applications written to support the faculty, staff, and students. Most of these have a SQL Server database to store the information. As with most shops, we have used various versions of SQL Server over the years to support our business partners. The old adage, “if it ain’t broke, don’t fix it” holds true for some of our older SQL Server instances. For those instances, we didn’t make an attempt to migrate off of them until it was required. Well, that time has come. We realized last year that SQL Server 2008 and 2008 R2 were losing their [extended support](https://blogs.msdn.microsoft.com/sqlreleaseservices/end-of-mainstream-support-for-sql-server-2008-and-sql-server-2008-r2/) and that would mean no more security updates. We didn’t want to increase our security risk to our data so we started the process of planning the migration to SQL Server 2016. 

\
After reviewing our database inventory, we found ~30 databases that needed to be migrated or decommissioned by July 9th, 2019. Having a hard deadline for a project is sometimes a nice way to back into the required tasks. But as we started looking through the databases, we realized that some of the apps that fronted the databases have not been touched in years. The first round of eliminations allowed us to ask questions like “Is this application still in use”. You would be surprised how many apps serve their purpose for a year or so and just fall off (similar to SSRS reports). 

\
We also started to realize that some of our applications had cross-references to other databases and that moving one database could break other applications. The review gave me a headache thinking about the dependencies and how we were going to approach the migrations. 

\
This is when it is time to dig deep and reach into my cookie jar for inspiration. I have found over the years that large problems can be easily solved by breaking them into smaller chunks. The quote that I use frequently is from a book written by Gary Keller and Jay Papasan titled “[The ONE Thing: The Surprisingly Simple Truth Behind Extraordinary Results](https://www.amazon.com/ONE-Thing-Surprisingly-Extraordinary-Results/dp/1885167776)”:

\
**“What’s the ONE Thing you can do such that by doing it everything else will be easier or unnecessary?”**

\
This sentence has helped me countless times starting on projects that seemed like monsters. It even helps me combat procrastination because by completing a simple step it helps me start down the path of project completion. 

\
I hope you can benefit from my cookie jar and keep it stored for your next monster project.
