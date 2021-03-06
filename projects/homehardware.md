---
title: HomeHardware Deliveries
subtitle: A delivery management App for Deka Home Hardware.
date: 2020-06-11
github: https://github.com/ccrowley96/HomeHardware
images:
    - /img/homehardware/homehardware1.png
    - /img/homehardware/homehardware2.png
    - /img/homehardware/homehardware3.png
tags: 
    - mongo
    - node
    - react
    - javascript
    - scss
---
Fork and re-write of [groceryList](/projects/grocerylist/).  I created this app for Deka Home Hardware in Ontario, CA.  It allows them to more easily track and manage deliveries.  Every day @ midnight EST, 7 delivery lists are created for each store.  Delivery list codes are created using the following format: **[w|c]mmddyy**, where w/c is the first character of each respective store.  For example, employees can view the delivery list for the Woodlawn store on 12/25/20 by typing w122520 and pressing 'join'.  This will create a new delivery list (if it doesn't already exist).  Employees can then add delivery items and mark them [picked | dispatched | complete | cancelled].  The site is live now (not linked for store privacy).