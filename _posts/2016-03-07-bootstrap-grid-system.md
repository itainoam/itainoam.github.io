---
title: Bootstrap Grid System
tags: [Development]
description:  Bootstrap Grid System
---
#### A few notes about the Bootstrap grid system

* Every page must have ```.container``` div for a wrapper
* The ```.container``` div adds padding of 15px on the left and right.
* ```.row``` nullifies the ```.container``` padding by setting a negative margin of -15px.
* Each ```.col``` adds 15px padding on the left and right.
*  ```.col-xs```/ ```.col-sm``` / ```.col-md``` / ```.col-lg``` define the size of the column per device.
* It's enough to only use ```.xs``` many times because a column defined for small devices will wor the same on all devices.
* ```.col-*-offset-*``` is used to leave spaces between columns.
