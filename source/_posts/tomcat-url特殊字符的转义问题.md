---
title: tomcat url特殊字符的转义问题
tags: tomcat
categories: 其它
date: 2019-01-03 10:56:15
---
get请求，url中带[]的话，tomcat的8.5以上的版本都不会自动转义，会返回400的错误。

之前的版本有的允许[],有的允许[]和{}，最新版本对url的要求更为严格。

可以通过修改tomcat的配置让url中可以使用[]

{% asset_img tomcatDoc1.jpg %}

{% asset_img tomcatDoc2.jpg %}

{% asset_img tomcatDoc3.jpg %}

可参考tomcat的源码

[](https://github.com/apache/tomcat/blob/trunk/java/org/apache/tomcat/util/http/parser/HttpParser.java)

最好的方法是发送请求时把特殊字符都转义好，axios提供提前转义的接口
Qs.stringify(params, {arrayFormat: 'repeat'})

```javascript
const defaultOptions = {
    baseURL: url,
    timeout: 20000, // 请求时间超过10秒视为超时
    headers: {'X-Requested-With': 'XMLHttpRequest'},
    withCredentials: true,
    paramsSerializer: function(params) {
        return Qs.stringify(params, {arrayFormat: 'repeat'});
    }
};
const axiosInstance = axios.create(defaultOptions);
```