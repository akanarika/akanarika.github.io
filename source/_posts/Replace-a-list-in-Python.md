---
title: Replace a list in Python
date: 2016-11-12 03:26:22
tags: [python]
---
Replace a list in Python:
```python
>>> l = [1,2,3]
>>> id(l)
4430796704
>>> l = [2,3]
>>> id(l)
4430918072
>>> l[:] = [1,2,3]
>>> id(l)
4430918072
```
The first way will change the id of the named list, while in the second way, only elements in the list are changed.
