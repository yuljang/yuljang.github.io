---
layout: single
title:  "\"Declaration\" in Python"
date:   2022-11-30 23:19:40 +0900
categories: GDSC
---

![Python logo](/assets/images/python.png)
<p align = "center">
Ah, my ol' friend, Python!
</p>
  

## Python, Again
In my previous post, I discussed about "is", "==" and their differences in Python (specifically, CPython). Python's behavior is strange compared to other languages in many situations. This post will also talk about one of those behavior.  
Disclaimer: I'm not posting to blame Python whatsoever. Python is one of my favorite languages.  

## Declaration
Many other languages, for instance Java, require declaration of variable before you can assign a value to it or use it.  

```Java
int Age;
Age = 20;
```

Of course, you can simultaneously declare and assign value to it.  

```Java
int Age = 20;
```

Still, it consists of two unique steps: declaration and assignment.  

## Declaration in Python...?

However, you never declare a variable in Python. You just assign value to whatever variable you want.  

```Python
age = 20 # "age" isn't declared beforehand
```

It's quite straightforward. Nothing strange about it. I agree. But it get a bit more confusing in classes.  

## Classes

Let's jump right into the problem. Following code does not cause error.

```Python
class Foo(object):
    pass

foo = Foo()
foo.bar = 5
```

Rather it's exactly equivalent to code below.

```Python
class Foo(object):
    def __init__(self, bar):
        self.bar = bar

foo = Foo(5)
```

Only difference is their use cases, so that you can force a class instance to have specific variable (in this case, bar).

