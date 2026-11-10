---
title: Deep modules
tags:
  - evergreen
  - software-design
---

A **deep module** gives you a lot of functionality behind a small, simple interface. The idea comes from John Ousterhout's *A Philosophy of Software Design*.

## Depth = benefit ÷ cost

Picture a module as a rectangle. The top edge is the **interface**: what callers must understand. The area is the **functionality**: what the module does for them.

```
  Deep module            Shallow module
  ┌──┐                   ┌──────────────────┐
  │  │                   │                  │
  │  │                   └──────────────────┘
  │  │
  │  │   small interface,       big interface,
  │  │   lots of work           little work
  └──┘
```

Every interface is a cost: things to learn, remember, and get wrong. A module is worth having when what it hides is much bigger than what it exposes.

## The classic example: Unix file I/O

```c
int  open(const char *path, int flags, mode_t mode);
ssize_t read(int fd, void *buf, size_t count);
ssize_t write(int fd, const void *buf, size_t count);
off_t lseek(int fd, off_t offset, int whence);
int  close(int fd);
```

Five calls. Behind them sit directory lookup, permissions, caching, disk scheduling, journaling, and dozens of filesystems and device types. Programmers have used this interface for decades without knowing any of that.

## Smells of a shallow module

> [!warning] Signs your module is shallow
> - The interface is about as complicated as the implementation.
> - Callers must call methods in a specific order to get anything done.
> - It's a "pass-through" wrapper that adds a name but no behaviour.
> - Configuration options push decisions onto the caller that the module could have made.

## Related ideas

- **Information hiding.** Each module should own a design decision and keep it secret.
- **"Classitis".** Lots of tiny classes look clean but add interface cost everywhere.
- [[ideas/Gall's law|Gall's law]]: grow working systems by deepening what exists, not by adding layers.
- [[ideas/Evergreen notes|Evergreen notes]] are deep modules for ideas: a short claim title on top, a lot of thinking underneath.
