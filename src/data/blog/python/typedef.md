---
title: Typedef in Python
pubDatetime: 2026-03-15T00:00:00Z
draft: false
tags:
  - python
  - typedef
  - type
  - alias
description: How to alias types
---

```python
type UserId = int
type Point = tuple[float, float]

def get_user(id: UserId):
    ...
```
