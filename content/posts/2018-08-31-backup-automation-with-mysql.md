---
title: "Backup automation with MySQL"
date: "2018-08-31T17:18:35"
slug: "backup-automation-with-mysql"
categories: ["Professional Development"]
---

One of our vendor applications we host on-premises was moving from SQL Server to MySQL (don’t get me started). Our responsibility was to make sure the MySQL databases were being backed up on a daily basis. I didn’t know the first thing about supporting MySQL but was looking forward to learning a new RDBMS to see how things worked.

My first stop was Plural Sight, Pinal Dave had a few MySQL courses I wanted to review to start understanding what it takes to support MySQL. I watched the following courses:

- MySQL Fundamentals
- MySQL Backup and Recovery Fundamentals
- MySQL Workbench Guided Tour

Pinal did a great job introducing me to MySQL and diving into all the areas I needed to understand how to support MySQL. Now that I had the basics, it was time to set up our MySQL backups. MySQL uses a command line tool to execute the backups, mysqldump.exe (insert joke here). MySQL backups are a bit different than SQL Server because the backup files are just text files with SQL statements to rebuild the database schema (DDL) and insert the data (DML).

I knew I could just create a simple Windows Tasks to run each night but I wanted something with some smarts. We have other RDBMS systems send us nightly emails with the status of the backup so we can review it during our morning checklist. My goals were to have the backup file have the date/time stamp within the filename, remove backups older than 30 days, and send an email with success/failure message. Time to hit the Google…

I found a great post with a sample Windows batch file that I started from. I forgot how powerful the Windows batch language was, you can do some pretty cool things (but PowerShell is much easier). I didn’t want to use ComMail from Microsoft, so I did another search for ways to send emails from Windows batch, and sure enough, PowerShell was the ticket. Looking back at this project, I should have started with PowerShell to build the backup script.

My next search was how to process return codes from the mysqldump.exe process. Now I had everything to build the process I needed. I took me a few hours of trial and error, but at the end of the day, we had a production-ready process. We have been running the scripts for a few weeks now and we have not had any issues. Remember, your backup is only as good as your restore.

Here is our batch file to manage the backups:

```batch
@echo off
c:
cd\
cd "Program Files\MySQL\bin"
 
For /f "tokens=2-4 delims=/ " %%a in ('date /t') do (set dt=%%c-%%a-%%b)
For /f "tokens=1-4 delims=:." %%a in ('echo %time%') do (set tm=%%a_%%b_%%c_%%d)
 
set bkupfilename=%dt% %tm%.sql
set logdir=E:\MySQLBackups
 
For /f "tokens=2-4 delims=/ " %%a in ('date /t') do (set dt=%%c-%%a-%%b)
For /f "tokens=1-4 delims=:." %%a in ('echo %time%') do (set tm=%%a:%%b:%%c:%%d)
set logtime=%dt% %tm%
 
echo Beginning MySQLDump Process > %logdir%\MySQLBackupLog.txt
echo Start Time = %logtime% >> %logdir%\MySQLBackupLog.txt
echo --------------------------- >> %logdir%\MySQLBackupLog.txt
echo Backing up to file: %bkupfilename% >> %logdir%\MySQLBackupLog.txt
 
mysqldump.exe --user=backup --password=backup --all-databases --single-transaction --flush-privileges >e:\mysqlbackups\"%bkupfilename%" 2>e:\mysqlbackups\DatabaseError.txt
 
if %errorlevel%==0 echo Backup success! >> %logdir%\MySQLBackupLog.txt
if %errorlevel%==0 del e:\mysqlbackups\DatabaseError.txt >> %logdir%\MySQLBackupLog.txt
if %errorlevel%==1 echo Backup warning, check DatabaseError.txt >> %logdir%\MySQLBackupLog.txt
if %errorlevel%==2 echo Backup error, check DatabaseError.txt >> %logdir%\MySQLBackupLog.txt
if %errorlevel%==3 echo Backup error, check DatabaseError.txt >> %logdir%\MySQLBackupLog.txt
if %errorlevel%==4 echo Backup error, check DatabaseError.txt >> %logdir%\MySQLBackupLog.txt
if %errorlevel%==5 echo Backup error, check DatabaseError.txt >> %logdir%\MySQLBackupLog.txt
if %errorlevel%==6 echo Backup error, check DatabaseError.txt >> %logdir%\MySQLBackupLog.txt
echo Errorlevel returned by mysqldump.exe %errorlevel% >> %logdir%\MySQLBackupLog.txt
 
For /f "tokens=2-4 delims=/ " %%a in ('date /t') do (set dt=%%c-%%a-%%b)
For /f "tokens=1-4 delims=:." %%a in ('echo %time%') do (set tm=%%a:%%b:%%c:%%d)
set logtime=%dt% %tm%
 
echo Done with MySQLDump >> %logdir%\MySQLBackupLog.txt
 
echo --------------------------- >> %logdir%\MySQLBackupLog.txt
echo MySQLDump Process Finished >> %logdir%\MySQLBackupLog.txt
echo End Time = %logtime% >> %logdir%\MySQLBackupLog.txt
echo --------------------------- >> %logdir%\MySQLBackupLog.txt
 
echo Deleting old backups >> %logdir%\MySQLBackupLog.txt
 
forfiles /p e:\mysqlbackups /s /m *.* /d -30 /c "cmd /c del @file : date >= 30days" >> %logdir%\MySQLBackupLog.txt
 
echo --------------------------- >> %logdir%\MySQLBackupLog.txt
dir %logdir%\*.* >> %logdir%\MySQLBackupLog.txt
echo Send email via PowerShell >> %logdir%\MySQLBackupLog.txt
 
powershell -executionpolicy Unrestricted -File "c:\software\SendEmail.ps1"
```

Here is our PowerShell file to send an email:

``` powershell
$smtp = “smtp.mysql.com"
$to = “dbasupport@mysql.com"
$from = “mysql@mysql.com" 
$attachment1="e:\mysqlbackups\mysqlbackuplog.txt"
$attachment2="e:\mysqlbackups\DatabaseError.txt"
 
if (Test-Path -path $attachment2)
{
    $subject = "MySQL Backup FAILED!!!!" 
    $body = "MySQL Backup failed, see attached logs for errors 
"    
    send-MailMessage -SmtpServer $smtp -To $to -From $from -Subject $subject -Body $body -BodyAsHtml -Attachments $attachment1, $attachment2
}
else
{
    $subject = "MySQL Backup Successful" 
    $body = "MySQL Backup Succedded
"
    send-MailMessage -SmtpServer $smtp -To $to -From $from -Subject $subject -Body $body -BodyAsHtml -Attachments $attachment1
}
```

If you run into any MySQL DBA responsibilities, I hope this gives you a starting point for managing your backups.
