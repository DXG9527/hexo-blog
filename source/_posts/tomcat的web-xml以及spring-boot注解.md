---
title: tomcat的web.xml以及spring-boot注解
tags:
  - java
  - tomcat
categories: JAVA
date: 2019-01-03 11:49:14
---
最近做文件上传遇到了一点问题，spring-boot框架，之前已经测试通过的文件上传突然后报错了，报上传文件为空的错误。
后台发现是因为tomcat的配置中加了web.xml，里面新添加了一些关于过滤的配置。去掉这个web.xml文件，上传又恢复正常。这是因为没有这个文件的时候tomcat会采用spring默认的配置，一旦加入了这个文件，tomcat会采用这个文件中的配置，一些用到的配置都必须要手动添加进来。
这一点有点像@EnableMVC注解的使用，加入了注解以后mvc的配置都会被重置，例如静态文件的访问配置都需要手动添加。
想要使用默认配置，无需使用 @EnaleWebMvc 注解。使用了 @EnableWebMvc 注解后 WebMvcAutoConfiguration 提供的默认配置会失效，必须提供全部配置。

回到文件上传的部分，在servlet 3的情况下，web.xml加入multipart-config的配置即可。

```xml
<servlet>
<servlet-name>dispatchServlet</servlet-name>
<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
<init-param>
<param-name>contextConfigLocation</param-name>
<param-value>WEB-INF/config/dispatch-servlet.xml</param-value>
</init-param>
<load-on-startup>1</load-on-startup>
<!-- 限制上传文件大小，单个 < 2M ;最多支持 10个文件(20M)-->
<multipart-config>
<max-file-size>2097152</max-file-size> <!-- 2*1024*1024 = 2097152 -->
<max-request-size>20971520</max-request-size> <!-- 10*2*1024*1024 = 20971520 -->
<file-size-threshold>0</file-size-threshold> <!--必填-->
</multipart-config>
</servlet>
```

只有servlet 3 才支持 multipart-config 配置

参考：[](https://docs.spring.io/spring/docs/3.2.x/spring-framework-reference/html/mvc.html#mvc-multipart)
