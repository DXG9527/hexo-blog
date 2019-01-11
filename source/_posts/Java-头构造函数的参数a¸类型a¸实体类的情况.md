---
title: Java 构造函数的参数类型为实体类的情况
date: 2018-12-24 17:41:28
tags:
---

当构造体的字段关联了其它的实体类，这个参数就要放在最后面，不然无法解析出它后面的参数，会报空指针的错误。

如
``` bash
public DmpNodePosition(float positionZ, DmpNodeInfo dmpNodeInfo) {
    this.dmpNodeInfo = new DmpNodeInfo(dmpNodeInfo.getId());
    this.positionZ = positionZ;
}

```

dmpNodeInfo应该放在最后一个参数的位置上。 