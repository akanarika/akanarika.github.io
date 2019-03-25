---
title: Reverse Linked List in Python
date: 2016-11-13 01:34:34
tags: [python]
---
A really fancy way to reverse a linked list in Python:
```python
def reverseList(head):
	new_head = None
	while head:
		head.next, head, new_head = new_head, head.next, head
	return new_head
```
