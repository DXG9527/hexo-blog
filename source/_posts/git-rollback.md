---
title: git rollback
tags: git
categories: 其它
date: 2019-01-03 11:36:32
---
merge的提交在sourceTree上没有办法直接revert，会报下面这个错，原因可能是merge自动提交，不会输入commit内容

```
Commit 1c3268d4b69dc6ca9dd89e92b513f5edb194978c is a merge but no -m option was given
```

解决方法：
```bash
git revert -m 1 <commit-hash> 
git commit -m "Reverting the last commit."
git push -u origin master
```

参考：[](https://stackoverflow.com/questions/49314451/revert-back-on-git-but-a-merge-but-no-m-option-was-given)