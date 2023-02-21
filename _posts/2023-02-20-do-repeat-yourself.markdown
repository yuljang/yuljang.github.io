---
layout: single
title:  "Do Repeat Yourself"
date:   2023-02-20 19:42:11 +0900
categories: GDSC
---


One of basic principles of programming is DRY (Don't Repeat Yourself). Well, it's kind of obvious since "computer" is invented to deal with same boring things. However, when it comes to understandable and maintainable code, it isn't always the case.

When I just started learning Go, the error handling code block bothered me little bit. 

```go
if err != nil {
  return nil, err
}
```

I had to type this code block everytime. However, after reading few articles and posts, I found that this might be actually a good thing for few reasons. 

## You HAVE TO Do it
The fact that it is have-to make you think about how your resources and logics are organized. It is because if you don't know what your code is doing, you surely don't know how to handle the errors from it. It's like a friend who reminds you important things in annoying ways. 

## Understandability

Do you like this?

```javascript
i = i ? i < 0 ? Math.max(0, len + i) : i : 0;
```

Well, I don't. I don't like the lines of code smashed into a line with unappreciated effort. I prefer the code where a line of code represent the work of "a line" worth. In same sense, when returning error, you should do it as is, otherwise you will have hard time later.
