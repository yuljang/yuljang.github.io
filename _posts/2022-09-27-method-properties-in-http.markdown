---
layout: single
title:  "Method Properties in HTTP"
date:   2022-09-27 15:42:21 +0900
categories: GDSC
---

![Tim Berners-Lee](/assets/images/tim-berners-lee.jpg)
<p align = "center">
Sir Tim Berners-Lee
</p>

[RFC 7231](https://www.rfc-editor.org/rfc/rfc7231#section-4.2) defines common method properties in HTTP and tells us which method has such properties. For the sake of simplicity, this post will only cover primary HTTP methods related to CRUD operation.


## Safe

> Request methods are considered "safe" if their defined semantics are essentially read-only; i.e., the client does not request, and does not expect, any state change on the origin server as a result of applying a safe method to a target resource.

Only GET method is considered safe. POST and PUT sends request body and DELETE doesn't, but all three expect the server to make change with their request.  


## Idempotent

> A request method is considered "idempotent" if the intended effect on the server of multiple identical requests with that method is the same as the effect for a single such request.

Idempotent could be a bit confusing, so I'll give you an example. A constant function $$ f(x) = c $$ is idempotent since $$ f(x) = f(f(x)) = \;...\;  = c $$. Same goes for HTTP methods. If a method is considered idempotent, server should be same as it is after initial request, regardless how many times requested. 

The result of PUT method

```http
PUT /user/1 {"name": "Timothy"}
```

will be same as

```http
PUT /user/1 {"name": "Timothy"}
PUT /user/1 {"name": "Timothy"}
PUT /user/1 {"name": "Timothy"}
```

making PUT idempotent.

In the same way, GET and DELETE method are also idempotent. However, POST method is different. With POST method, the server handles request with its own semantics which possibly makes changes after each reqeust. Hence, POST is not idempotent. 

As an oversimplified example,

```http
POST /user {"name": "Yul"}
```

will make new user named "Yul" with its own user_id. Then,


```http
POST /user {"name": "Yul"}
POST /user {"name": "Yul"}
POST /user {"name": "Yul"}
```

will make three unique users named "Yul" with different user_id, and the result is not the same. 


## Cachable

> Request methods can be defined as "cacheable" to indicate that responses to them are allowed to be stored for future reuse

Even though this property is listed as common method property, caching related topics are way more complicated. I will not cover this property in this post as it will be whole another post. If you are interested, check [RFC 7234](https://www.rfc-editor.org/rfc/rfc7234).  


## Property Table

| Method 	| Safe 	| Idempotent 	|
|:------:	|:----:	|:----------:	|
|   GET  	|  yes 	|     yes    	|
|  POST  	|  no  	|     no     	|
|   PUT  	|  no  	|     yes    	|
| DELETE 	|  no  	|     yes    	|

<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>