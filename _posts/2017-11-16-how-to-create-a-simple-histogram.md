---
layout: post
title: "TIL: How to create a simple histogram to see a trend in data"
description: You can use SQL for generating simple histograms.
summary: You can use SQL for generating simple histograms.
tags: til sql
date: 2017-11-16
---

## How many unique users were created each month

```
SELECT EXTRACT(YEAR FROM created_at) as year,
       EXTRACT(MONTH FROM created_at) as month,
       COUNT(DISTINCT(email)),
       LPAD('', (COUNT(DISTINCT(email))/100)::int, '#') as frequency
FROM users
GROUP BY 1,2;
```

```
 year | month | count | frequency
------+-------+-------+-----------
 2016 |     1 |   500 |
 2016 |     2 |  1000 | #
 2016 |     3 |  1100 | #
 2016 |     4 |  1200 | #
 2016 |     5 |  2000 | ##
 2016 |     6 |  3000 | ###
 2016 |     7 |  2000 | ##
 2016 |     8 |  2000 | ##
 2016 |     9 |  5000 | #####
 2016 |    10 |  5500 | #####
 2016 |    11 |  5000 | #####
 2016 |    12 |  1000 | #
```
