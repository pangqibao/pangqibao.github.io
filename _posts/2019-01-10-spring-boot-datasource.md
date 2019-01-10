---
layout: post
title: spring boot datasource
date: 2019-01-10 11:25:00 +0300
description: spring boot 链接数据库
img: software.jpg # Add image post (optional)
categories: [spring boot,java]
tags: [spring,java, spring boot] # add tag
---

任何一个程序都少不了要数据库的操作，而spring boot中链接数据库超级简单。

我们需要在application.properties中进行配置，application.properties路径是src/main/resources下，对于application.properties的更多介绍请自行搜索资料，或者我会在后面介绍，好了不多说，以下只是mysql的配置，其他数据库类似。

> 大体步骤
>
> (1)在application.properties中加入datasource的配置
>
>(2)在pom.xml加入MySQL的依赖
>
>(3)获取DataSource的Connection进行测试

src/main/resource/application.properties
```
########################################################
###datasource
########################################################
spring.datasource.url=jdbc:mysql://localhost:3306/test
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driverClassName=com.mysql.jdbc.Driver
spring.datasource.max-active=20
spring.datasource.max-idle=8
spring.datasource.min-idle=8
spring.datasource.initial-size=10
```
pom.xml配置：
```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>
```
到此相关配置就结束了，那么就可以在项目中进行测试链接了。
