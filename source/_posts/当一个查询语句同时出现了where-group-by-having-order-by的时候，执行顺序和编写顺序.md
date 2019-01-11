---
title: '当一个查询语句同时出现了where,group by,having,order by的时候，执行顺序和编写顺序'
date: 2018-12-27 17:25:56
tags:
---
1.执行where xx对全表数据做筛选，返回第1个结果集。
2.针对第1个结果集使用group by分组，返回第2个结果集。
3.针对第2个结果集中的每1组数据执行select xx，有几组就执行几次，返回第3个结果集。
4.针对第3个结集执行having xx进行筛选，返回第4个结果集。
5.针对第4个结果集排序。

[](http://blog.csdn.net/superhosts/article/details/39298529)