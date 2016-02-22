---
title: Generating Lines Of Code Report
tags: [JavaScript]
description: Generating Lines Of Code Report
---
In order to compare two projects I needed to count LOC. This command generates a report and saves it to CSV.

```
npm install - g cloc
cloc . --global --exclude-dir=bower_components,common,stylesheets,ihub,.idea --csv --out=loc.csv
```
