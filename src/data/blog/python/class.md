---
title: Python Classes
pubDatetime: 2026-03-11T00:00:00Z
draft: false
tags:
  - python
description: Python classes, objects, properties and methods reference.
---

### Classes, objects, properties and methods
```python
class Car:
    # ────────────────────────────────────────────────
    #  Class variables  (shared by all instances)
    # ────────────────────────────────────────────────
    wheels       = 4             # most common style
    all_cars     = []            # mutable class variable – be careful!
    _counter     = 0             # "protected" by convention

    DEFAULT_COLOR = "silver"     # often written in UPPER_CASE when constant-like

    # ────────────────────────────────────────────────
    #  Alternative constructor(s)  →  @classmethod
    # ────────────────────────────────────────────────
    @classmethod
    def from_color(cls, color: str) -> "Car":
        """Alternative constructor – very idiomatic use-case"""
        obj = cls()                  # cls == Car (or subclass)
        obj.color = color
        return obj

    @classmethod
    def create_default(cls) -> "Car":
        return cls(color=cls.DEFAULT_COLOR)

    # ────────────────────────────────────────────────
    #  "Utility" / pure functions inside the namespace  →  @staticmethod
    # ────────────────────────────────────────────────
    @staticmethod
    def is_valid_license_plate(plate: str) -> bool:
        """Doesn't need self or cls – just lives in the namespace"""
        return len(plate) >= 5 and plate.isalnum()

    # ────────────────────────────────────────────────
    #  Normal initializer
    # ────────────────────────────────────────────────
    def __init__(self, make: str, model: str, *, color: str | None = None):
        # ──────────────────────────────
        #  Instance variables  (per-object)
        # ──────────────────────────────
        self.make      = make
        self.model     = model
        self.color     = color or self.DEFAULT_COLOR   # ← safe access to class var
        self.mileage   = 0
        self._vin      = None                          # private by convention

        # Updating class variable (if that makes sense)
        type(self)._counter += 1           # better than Car._counter
        type(self).all_cars.append(self)   # ← common pattern (but be cautious)

    # ────────────────────────────────────────────────
    #  Instance methods  (most common – work with self)
    # ────────────────────────────────────────────────
    def drive(self, km: float) -> None:
        self.mileage += km

    def description(self) -> str:
        return f"{self.color} {self.make} {self.model} ({self.mileage:,} km)"

    @property
    def age(self) -> int:               # ← very idiomatic
        """Example property – computed on the fly"""
        from datetime import date
        return date.today().year - 2020   # pretend manufacturing year = 2020

    def __str__(self) -> str:
        return self.description()

    # Optional: cleanup class-level collection when instance dies
    def __del__(self):
        type(self).all_cars.remove(self)
        type(self)._counter -= 1
```
