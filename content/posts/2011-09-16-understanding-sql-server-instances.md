---
title: "Understanding SQL Server Instances"
date: "2011-09-16T11:08:39"
slug: "understanding-sql-server-instances"
categories: ["SQL Server"]
tags: ["64bit", "browser", "DBA", "domain", "Enterprise", "ESX", "firewall", "instance", "netstat", "physical", "server", "SSCM", "Standard", "TCP", "UDP", "virtualization", "VM"]
archived_comments: [{"author": "Tanuj Narula", "date": "2011-09-23 21:38:51", "text": "Hey Vishal,\n\nNice write up, keep it going...\n\nTanuj Narula"}]
---

Being raised within SQL Server 6.5 & 7.0, SQL Server instances were not available in those versions.  I never fully understood the advantage of having multiple instances on the same server so I never embraced it.  I always had a single, default instance per physical server.  Once I got involved with virtualization a few years ago, having multiple instances of an OS running on a single physical server finally got me thinking about multiple instances of SQL Server.

My lab at home has been the perfect place to install, configure and understand multiple SQL Server instances.  I have two servers running ESXi 4.1 U1 and VM's to support a small Windows Domain.

I started with a copy of Windows Server 2008 R2 64bit as the guest OS.  I installed my first copy of SQL Server 2005 Standard under a named instance of SQL03\SQL2005Standard (I currently don't have a standard instance of SQL Server installed on this VM).  I then proceeded to install SQL Server 2005 Enterprise, SQL Server 2008 Standard & SQL Server 2008 Enterprise all as named instances on the same VM as SQL03\SQL2005Ent, SQL03\SQL2008Standard, SQL03\SQL2008Ent, respectively.

Here is what I learned about supporting multiple instances of SQL Server from a DBA point of view:

- The default instance of SQL Server, known as MSSQLSERVER, runs under TCP port 1433
- Under Windows Server 2008, the firewall is enabled by default so you need to create inbound rules to allow outside connections to be able to reach SQL Server.
- SQL Server Browser service is responsible for taking requests for named instances and forwarding them to the correct port, whether it's dynamic or statically configured.  If there are no named instances of SQL Server, the Browser service is not required.
- The SQL Server Browser service runs under UDP port number 1434.  This will need to be opened under the firewall.
- With out the SQL Server Browser service running, you would need to provide the IP and Port number (xxx.xxx.xxx.xxx:yyyy) in order to connect to a SQL Server instance.
- To connect to a SQL Server instance by name, you use the \<computer name\>\\\<instance name\> syntax.
- By default, named instances are set to dynamic ports.  This causes an issue trying to open ports on the Windows firewall because each time SQL Server is restarted a new port can be set.  With the firewall enabled, it's best to switch to static ports for all named instances and then create inbound rules for those TCP ports.
- If you prefer to use dynamic ports, you can also exclude the sqlserver.exe process from the firewall.  This would allow inbound connections for just the SQL Server process and thus all clients to connect to dynamic or static ports without having to create individual rules for each TCP port number.
- To set an instance to a static port, open SQL Server Configuration Manager (SSCM) and drill through SQL Server Network Configuration and expand the Protocols tree for your named instance.  Right click on TCP/IP and select Properties.  Click on the IP Address tab and scroll all the way to the bottom of the list until you see 'All IP'.  Clear out the TCP Dynamic box and under TCP Port, provide the desired TCP port number.  To switch back to dynamic port allocation, just clear out the TCP Port box and place a zero in the TCP Dynamic box.  Any time you make a change to the Protocol settings, you will need to restart the SQL Server service for the named instance.
- TCP and UDP ports are registered with a national directory.  You can reference them by using this Wikipedia [article](http://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers).  I chose to use TCp ports 1435 through 1438 for my instances.  Well known ports are from 0 - 1023, Registered ports are from 1024 - 49151, and Dynamic ports are from 49152 - 65535.
- To see a list of ports the server is using, run 'netstat -an' from the command prompt.  Use this data along with available ports from Wikipedia to determine what ports are available on your system.

I hope you find this useful when you try to install SQL Server with multiple instances when the Windows Firewall service is enabled.
