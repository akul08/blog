---
layout: post
title: "Shallow v/s Deep copy"
comments: true
description: "Shallow vs Deep copy and when to use which."
keywords: "shallow, deep, copy, python, reference, new object, duplicate"
---
---

## What is Copy?

An object copy is a process where a data object has its attributes copied to another object of the same data type. In Python, Shallow copy and deep copy are used for copying data between objects.

---

### Copy module of Python

Assignment statements in Python do not copy objects, they create bindings between a target and an object. For collections that are mutable or contain mutable items, a copy is sometimes needed so one can change one copy without changing the other. This module provides generic shallow and deep copy operations.


`# python`

    import copy
    copy.copy(x) # Return a shallow copy of x.
    copy.deepcopy(x) # Return a deep copy of x.
    exception copy.error
        # Raised for module specific errors.
---

### The difference between shallow and deep copying is only relevant for compound objects (objects that contain other objects, like lists or class instances):

| Shallow Copy | Deep Copy |
| --- | --- |
| constructs a new compound object and then (to the extent possible) inserts references into it to the objects found in the original. |  constructs a new compound object and then, recursively, inserts copies into it of the objects found in the original. |
| Shallow copies duplicate as little as possible. A shallow copy of a collection is a copy of the collection structure, not the elements. With a shallow copy, two collections now share the individual elements. | Deep copies duplicate everything. A deep copy of a collection is two collections with all of the elements in the original collection duplicated. |

### Infographics

|Example| Example|
|--- | ---|
| 1 | 2 |
| ![Difference1](http://i.stack.imgur.com/hOPkR.png) |  ![Difference2](http://i.imgur.com/oPTzEJs.jpg?1) |

### Summary

In short, shallow copy creates reference to the original object, two variables refer to the same area of memory. Later modifications to the contents of either are instantly reflected in the contents of other, as they share contents.

Whereas deepcopy, creates a new object with copy of original values of object. The values in the memory area which one points to are copied into the the memory area to which another points. Later modifications to the contents of either remain unique. The contents are not shared.
