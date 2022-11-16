---
layout: single
title:  HTTP Timeout and Long Polling
date:   2022-11-16 16:23:53 +0900
categories: GDSC
---

![408 Timeout](/assets/images/408.jpg)
<p align = "center">
</p>


## HTTP is stateless but...
HTTP is stateless protocol which means that every HTTP request is independent and does not relate to each other. At first, and still most of the time today, it is very useful. It simplified and made so much easier to communicate. 
However, modern web application requires connection between a server and a client. Without connection, the server is able to talk (send a data) only when client send a request. 
There are other alternatives such as HTML5 Websocket nowadays, but it was needed implement connection in HTTP environment at that time.


## Polling
Polling is a technique that a client constantly sends a request to a server to hear if there is datas the server wants to send. In this way, it can "mock" the connection. Though it isn't real-time, its near-real-time is good enough for majority of applications. 
One of its major drawback is overhead of HTTP request. Header of HTTP is called header cause it's not the body. ...What I mean is that header content is barely or not at all related to the data in the body server wanted to send.
What they found to handle this was...


## Timeout
There is a timeout for every HTTP request. If timeout is set 100 seconds, 100 seconds without response results in 408 timeout error. People did not focus on error. They focused on "100 seconds". In other words, the client who sent HTTP request keeps the connection alive waiting response from the server. It basically makes a client a server during timeout period.


## Long Polling
In long polling, a client sends a request to a server. And the server doesn't respond immediately but waits untl timeout occurs (or send some arbitrary response that says nothing). Then a client make anothe r request and repeat. This technique significantly reduced overhead. From few request a second to a request to 100~ seconds.

