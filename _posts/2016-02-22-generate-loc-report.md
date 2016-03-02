---
title: Generating Lines Of code report
tags: [JavaScript]
description: Keep large libraries sane using Browserify. With ES6 and CoffeeScript support!
---
In order to compare two projects I needed compare LOC. This command generates a report and saves it to CSV.

```
NPM install - g cloc
cloc . --global --exclude-dir=bower_components,common,stylesheets,ihub,.idea --csv --out=loc.csv
```
