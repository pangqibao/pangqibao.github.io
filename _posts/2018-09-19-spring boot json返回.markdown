---
layout: post
title: spring boot json返回
date: 2018-09-19 17:40:00 +0300
description: spring boot json 返回
img: software.jpg # Add image post (optional)
categories: [spring boot,java]
tags: [spring,java, spring boot] # add tag
---

<font color="red">（注：这篇文章不是最好的方式，可以废弃不读，在章节66.spring boot完美使用Fast Json解析JSON数据，提供更完美的方案。）</font>

在做如下操作之前，我们对之前的hello进行简单的修改，我们新建一个包com.example.demo.controller 然后新建一个类HelloController，然后修改DemoApplication.java类，主要是的这个类就是一个单纯的启动类。
主要代码如下

DemoApplication.java
```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

/**
 * @SpringBootApplication 声明让spring boot自动给程序进行必要的配置，等价于以默认熟悉使用
 * @configuration，@EnableAutoConfiguration和@ComponentScan
 */
@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```
HelloController.java
```java
package com.example.demo.controller;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @RequestMapping("/")
    public String hello(){
        return "hello";
    }
}
```
运行代码和之前是一样的效果。

我们在编写接口的时候，时常会有需求返回json数据，那么在spring boot应该怎么操作呢？主要是在class中加入注解@RestController.

<font color="red">**返回JSON之步骤**</font>
1. 编写一个实体类Demo；
2. 编写DemoController；
3. 在DemoController加上@RestController和@RequestMapping注解；
4. 测试

具体代码如下
com.example.demo.bean.DemoBean
```java
package com.example.demo.bean;

/**
 * 测试实体类
 */
public class DemoBean {
    /**
     * 主键
     */
    private Integer id;
    /**
     * 测试名称
     */
    private String name;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

```

com.example.demo.controller.JsonDemoController
```java
package com.example.demo.controller;

import com.example.demo.bean.DemoBean;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

/**
 * 测试返回json数据
 */
@RestController
@RequestMapping("/demo")
public class JsonDemoController {
    /**
     * 返回demo数据
     * 请求地址：http://localhost:8080/demo/getDemo
     * @return
     */
    @RequestMapping("/getDemo")
    public DemoBean getDemo(){
        DemoBean demoBean=new DemoBean();
        demoBean.setId(1);
        demoBean.setName("测试");
        return demoBean;
    }
}

```
启动，运行，在浏览器地址栏输入：http://localhost:8080/demo/getDemo返回如下数据
```json
{
    "id":1,
    "name":"测试"
}
```
spring boot也是引用了JSON解析包Jackson，那么自然我们就可以在Demo对象上使用Jackson提供的json属性的主键，对时间进行格式化，对一些字段进行忽略等。
