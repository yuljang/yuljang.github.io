---
layout: single
title:  "\"is\" and \"==\" in Python"
date:   2022-10-12 16:13:53 +0900
categories: GDSC
---

![Cythen Logo](/assets/images/cython-logo.png)
<p align = "center">
</p>

Python uses `and` and `or` instead of `&&` and `||`. Whether you are a beginner or not, can't deny that it's more readable and more aesthetic (I know, it's controversial). 

Similarly, both `is` and `==` exist in Python. In a nutshell, `is` compares objects' identities while `==` compares objects` values (it's actually more complicated). This gives us another question: what is an object in Python?

Almost Everything in Python is an object: primitives, functions, methods... except some exceptions including keywords (e.g. `if`). If you declare two variables, they are two different objects referenceing difference values. I will skip about CPython's definition and implementation of an object. 

I think I get it! So...

```python
>>> x = 1
>>> y = 1
>>> x == y
True
>>> x is y
True # What? 
```

Ah! I forgot to tell you that Python (technically, CPython) does "pre-allocation" for small integers ranging `[-5, 256]`. So if two variables' value is a same integer from -5 to 256, their references are same. 

Alright, then for string..

```python
>>> x = 'a'
>>> y = 'a'
>>> x == y
True
>>> x is y
True # Again?
```

Sorry, I forgot another thing. Python interpreter also checks if the assigned value already exists in the heap. 

Ok...

```python
>>> x = 'thisisverylongstring!^^'
>>> y = 'thisisverylongstring!^^'
>>> x == y
True
>>> x is y
False # Now it seems right...
```

There were few exceptions but everything seems right...?

```python
>>> x = 'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa'
>>> y = 'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa'
>>> x == y
True
>>> x is y
True # ???

>>> for i in range(5):
...     x = 'a' * i
...     y = 'a' * i
...     print(x is y)
True  # i = 0 
True  # i = 1
False # i = 2 ???
False # i = 3 ???
False # i = 4 ???
```

And there are A LOT more examples like these. Why this happens? That's tough question, but well, for performance I assume. When this happens? That's tougher question, and I can't really answer. If you really want to find out, you probably have to look at [CPython implementation source code](https://github.com/python/cpython/tree/main). In other words, these questions are not part of python itself, but it's implementation specific. If it's PyPy or Jython, the results of examples above may or may not be completely different. 

Moral of the story: use `==` if you can, use `is` if you have to.
