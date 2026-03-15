---
title: Interfaces in Python
pubDatetime: 2026-03-13T00:00:00Z
draft: false
tags:
  - python
  - interface
  - abstract
  - trait
  - mixin
description: How-to program to an interface in python
---

### The "Java-Style" explicit way: Abstract Base Classes (ABCs)

```python
from abc import ABC, abstractmethod

# Think of these as your Interfaces
class Flyable(ABC):
    @abstractmethod
    def fly(self):
        pass

class Swimmable(ABC):
    @abstractmethod
    def swim(self):
        pass

# Implementing multiple "interfaces"
class Duck(Flyable, Swimmable):
    def fly(self):
        print("Flap flap!")

    def swim(self):
        print("Paddle paddle!")

# This will raise a TypeError if you forget to implement fly() or swim()
d = Duck()
```

### The "Go-style" implict way with Protocols (Structural Subtyping)
```python
from typing import Protocol

class Drawable(Protocol):
    def draw(self) -> None:
        ...

class Shape:
    def draw(self) -> None:
        print("Drawing a shape")

# 'Shape' implements 'Drawable' even though it doesn't explicitly inherit from it.
def render(obj: Drawable):
    obj.draw()

render(Shape())
```
