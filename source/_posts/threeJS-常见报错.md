---
title: threeJS 常见报错
date: 2018-12-27 17:36:54
tags:
---
THREE.Matrix3.getInverse(): can't invert matrix, determinant is 0
可能错误原因
源码
```bash
        // no inverses  
        // 没有逆矩阵  
  
        if ( det === 0 ) {  
  
            var msg = "Matrix3.getInverse(): can't invert matrix, determinant is 0";    //提示用户该矩阵没有逆矩阵  
  
            if ( throwOnInvertible || false ) {  
  
                throw new Error( msg );  
  
            } else {  
  
                console.warn( msg );  
  
            }  
  
            this.identity();    //获得一个单位矩阵  
  
            return this;    //返回单位矩阵  
  
        }  
```

发生可能原因
mesh.scale.x(或y或z)为0
object.scale is a Vector3

参考:[](https://stackoverflow.com/questions/19150120/scaling-an-object-in-three-js)