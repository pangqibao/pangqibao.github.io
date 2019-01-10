---
layout: post
title: spring boot datasource
date: 2019-01-10 11:25:00 +0300
description: spring boot �������ݿ�
img: software.jpg # Add image post (optional)
categories: [spring boot,java]
tags: [spring,java, spring boot] # add tag
---

�κ�һ�������ٲ���Ҫ���ݿ�Ĳ�������spring boot���������ݿⳬ���򵥡�

������Ҫ��application.properties�н������ã�application.properties·����src/main/resources�£�����application.properties�ĸ�������������������ϣ������һ��ں�����ܣ����˲���˵������ֻ��mysql�����ã��������ݿ����ơ�

> ���岽��
>
> (1)��application.properties�м���datasource������
>
>(2)��pom.xml����MySQL������
>
>(3)��ȡDataSource��Connection���в���

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
pom.xml���ã�
```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>
```
����������þͽ����ˣ���ô�Ϳ�������Ŀ�н��в��������ˡ�
