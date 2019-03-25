---
title: '''Is None'' vs ''== None'' in Python'
date: 2016-10-17 19:56:12
tags: [python]
---
The reason for choosing
```python
egg is None
```
over
```python
egg == None
```
is: The operator "==" can be overloaded, and is likely to break when comparing valid object with None, while "is" always works the same.

reference page:
[Stack Overflow Answer]("http://stackoverflow.com/questions/3289601/null-object-in-python")

