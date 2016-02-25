---
title: This Keyword in Javascript
tags: [JavaScript]
description: This Keyword in Javascript
---
The value of the ```this```keyword is determined in this order of precedence:

1. When a new function is created with the ```new``` keyword it is set to that function.
2. When specfied explictly with ```.apply``` or ```.call``` it set to the specified argument.
3. When owened by an object it will be set to that object. 
4. Otherwise it is set to ```undefined``` (or global variable when not in ```'strict mode'```).

