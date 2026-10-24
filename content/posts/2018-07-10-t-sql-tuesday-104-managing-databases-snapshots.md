---
title: "T-SQL Tuesday #104 - Managing Databases Snapshots"
date: "2018-07-10T18:44:11"
slug: "t-sql-tuesday-104-managing-databases-snapshots"
categories: ["SQL Server"]
---

[<img src="/wp-content/uploads/2017/12/sqltuesday.png" class="alignleft wp-image-662 size-full" width="129" height="130" />](https://bertwagner.com/2018/07/03/code-youd-hate-to-live-without-t-sql-tuesday-104-invitation/)This month’s \#tsql2sday is being hosted by Bert Wagner ([b](https://bertwagner.com)\|[t](https://twitter.com/bertwagner)). His topic is about code we have written that we would hate to live without.

We have a pretty good handle on change control here and one of the steps we perform before any change is made to a database is to take a [database snapshot](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-snapshots-sql-server?view=sql-server-2017). Database Snapshots used to be an Enterprise only feature, but with the release of 2016 SP1, it is now available under Standard, Web, and Express editions. If you have been using Standard Edition for a while, you may not have realized this feature is available to you.

Database snapshots are read-only versions of the database at the time the snapshot was taken. Database snapshots start off at almost a zero byte databases. It is only when changes occur to the original database that the original pages are copied to the database snapshot. Let’s say you took a database snapshot at 2:00 pm, after that point, before any pages are modified in the original database, the unaltered pages are copied to the snapshot database. This process enables you to keep an ‘as-of view’ of the database, in this example as of 2:00 pm. The snapshot database is visible under SSMS and you can see the schema/data just like it was a live database. The big difference is the snapshot database is read-only and only grows as data pages are modified in the original database.

When you create a database snapshot before a schema or data change request, you are enabling yourself to have visibility into the database just before the change. Just imagine if you had an UPDATE or DELETE change go south, with the database snapshot in your back pocket, you can pull the original data from the snapshot database or [restore the database from the database snapshot](https://docs.microsoft.com/en-us/sql/relational-databases/databases/revert-a-database-to-a-database-snapshot?view=sql-server-2017).

Because of the number of databases and changes we manage, we keep up with a shared script that has all the scripts for the last database snapshots. This makes it easy to create a new database snapshot without having to re-create the T-SQL each time. Here is an example of what a create database snapshot statement looks like.

``` sql
CREATE DATABASE DBA_ss_20180703_0858 ON
(NAME=DBA,FILENAME=
'D:\SQLData\DBA_20180703_0858.ss'),
(NAME=DBA_data1,FILENAME=
'D:\SQLData\DBA_data1_20180703_0858.ss'),
(NAME=DBA_data2,FILENAME=
'D:\SQLData\DBA_data2_20180703_0858.ss'),
(NAME=DBA_data3,FILENAME=
'D:\SQLData\DBA_data3_20180703_0858.ss'),
(NAME=DBA_data4,FILENAME=
'D:\SQLData\DBA_data4_20180703_0858.ss')
AS SNAPSHOT OF DBA;
```

If you need help with understanding where your database files are located, you can use EXEC sp_helpfile under the context of your database. This will return the necessary information to build your CREATE DATABASE AS SNAPSHOT statement. We chose to key the snapshot files in the same folder structure as the MDF/LDF files.

We generally keep our snapshots for 3 business days. To keep track of all the database snapshots across our instances, we run a query against one of our [Central Management Server](https://docs.microsoft.com/en-us/sql/relational-databases/administer-multiple-servers-using-central-management-servers?view=sql-server-2017) folders on a weekly basis and delete the older database snapshots.

``` sql
SELECT name
FROM sys.databases d
WHERE d.source_database_id IS NOT NULL;
```

I hope you can see the advantage of database snapshots and keeping a history of the T-SQL used to create all your database snapshots. One of the main goals of a Database Administrator is keeping the data safe and database snapshots do the job for us.
