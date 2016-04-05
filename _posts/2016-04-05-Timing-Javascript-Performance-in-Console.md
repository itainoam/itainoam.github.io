---
title: Timing a 
tags: [JavaScript]
description:  Timing Javascript Performance in Console 
---

While wrangeling data with lodash I was wondering how long it all takes.

Turns out it's really easy:

```
console.time("perfTest");

// some code

console.endTime("perfTest");
```
