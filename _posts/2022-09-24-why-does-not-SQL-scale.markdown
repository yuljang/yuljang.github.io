---
layout: single
title:  "Why does not SQL scale?"
date:   2022-09-21 11:01:26 +0900
categories: GDSC
---

SQL and NoSQL have a lot of differences. Data validity, performance, storage efficiency, and so on. In this post, I want to discuss about their scalability. In general, SQL scales vertically (scale-up), whereas NoSQL scales horizontally (scale-out). Horizontal scaling is known to be more scalable than vertical scaling for various reasons: cost performance trade-offs, single point of failure, etc. 

So I just claimed that SQL does not scale, and NoSQL scales. But why?

## Normalization
To be a relational database, its data has to be normalized all across the database. This normalization process reduces data redundancy and improve data integrity. Also, its storage efficiency is high because there is no duplication of data. However, it comes with disadvantage. Since there is no duplication of data, you might have to travel many tables in order to find the value you're looking for. NoSQL, instead, intentionally duplicate data to speed up the queries. In this way, you can optimize the placement of data (not the query itself!) so that fewer or simpler query is just the job.

## Sharding
Technically, its partitioning what makes NoSQL horizontally scalable, but I just used sharding as its most popular way to partition. In SQL, sharding is difficult to achieve than in NoSQL. Main reason is that you can't Join across different shards unless you have thoughtfully well designed application-level sharding. Additionally, even if you use sharding on SQL, it would come along with significant performance drawback because of the networking between the shards. 

## `Join` Operation
The notorious `Join` operation drags the performance down with its **O(m+n)** time complexity. To note, **O(m+n)** is already improved time complexity with Merge Join or Hash Join. Naive Nested Loop Join has time complexity of **O(mn)** (!). Besides that, this `Join` operation is not compatible with sharding or normalization despite the fact that Join operation is actually essence of SQL.

That's about it for today. Hope you enjoyed reading.