---
title: Gall's law
tags:
  - evergreen
  - systems
  - engineering
---

> [!quote] John Gall, *Systemantics* (1975)
> A complex system that works is invariably found to have evolved from a simple system that worked. A complex system designed from scratch never works and cannot be patched up to make it work. You have to start over with a simple working system.

## What it means in practice

You can't skip the simple version. Every complex working system you admire (the web, Linux, Git) started as something small that worked, then grew one working step at a time.

Big up-front designs fail because each component makes assumptions about the others, and none of those assumptions have been tested against reality. When the parts meet, the assumptions fail together.

## Examples

- **The World Wide Web** began as a few HTML pages on a single NeXT machine at CERN.
- **Linux** was announced in 1991 as "just a hobby, won't be big and professional".
- **This garden** started with one page. See [[ideas/Digital gardens]].

## Applying it

1. Build the thinnest slice that works end to end, even if it's ugly.
2. Keep it working at every step. Never take it apart for a big rewrite.
3. Grow it based on what actually breaks, not what you imagine will break.

This connects to:
- [[tech/Deep modules]]: once something works, deepen its modules instead of adding more surface area.
- [[tech/Home automation should be boring]]: a smart home is a complex system that has to keep working while you change it.
- [[tech/Dotfiles are a living document]]: a perfect config doesn't come from a single setup session.
