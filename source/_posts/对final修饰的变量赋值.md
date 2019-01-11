---
title: 对final修饰的变量赋值
date: 2018-12-27 17:27:34
tags:
---
If you want to do any operation on your final variable passed to your method then use any collection api like List.

```bash
public void experiment(final List<TimeTraveler> timeTraveler) {

 }
```
Now, you can modify the value inside your list.

如果想对final修饰的变量赋值，将该变量放到list里面，用final修饰list就可以了

map也可以