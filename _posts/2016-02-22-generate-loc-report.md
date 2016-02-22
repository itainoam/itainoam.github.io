---
title: Generating Lines Of Code Report
tags: [JavaScript]
description: Generating Lines Of Code Report
---
In order to compare two projects I needed to count LOC. The [cloc package](https://www.npmjs.com/package/cloc) (based on perl tool by the same name) can generate a report and save it to CSV.

```
npm install - g cloc
cloc . --global --exclude-dir=bower_components,common,stylesheets,ihub,.idea --csv --out=loc.csv
```
