---
title: "A little SQL Curry goes a long way"
date: "2018-05-03T17:56:35"
slug: "a-little-sql-curry-goes-a-long-way"
categories: ["Professional Development"]
---

<img src="/wp-content/uploads/2018/05/istock_000019639558_medium-300x200.jpg" class="size-medium wp-image-819 alignleft" width="300" height="200" />We hired a Director of Information Security a while back. One of the things that excited me the most about this new position was the ability to exchange ideas around security under SQL Server. Our initial discussion was over lunch at a local Indian restaurant, Taaza Bistro ([w](https://taazabistro.com)\|[t](https://twitter.com/taazabistro)), and I found it very beneficial. We talked about our best practices and from that we agreed that there wasn't any immediate need for us to alter our course (that was good news).

From that initial conversation, we continue to get together at the same restaurant every other month or so to talk about new ideas, active and future projects, or changes in the industry. The nice part about these lunches is the ability to bounce around ideas from a pure security standpoint. I leave each lunch with a better take on how to architect more secure solutions with SQL Server.

Our latest project is using a [proxy server](https://en.wikipedia.org/wiki/Proxy_server) for all of our SSIS SFTP transmissions to vendors. The advantage of using proxies is they can lower your risk footprint by not have egress connections directly from your secure network. This allows you to place the proxy box under the DMZ for outbound connections.

The one thing I wanted to relay from this experience is how these lunches can be helpful for other databases administrators. It may not be with your Security Director, but it could be with the service desk, SAN/Domain admins, or any other department in your organization that you don't normally speak to daily basis. It's a great way to bounce ideas and understand pain points from other co-workers.

Here’s to plenty more SQL Curry lunches!
