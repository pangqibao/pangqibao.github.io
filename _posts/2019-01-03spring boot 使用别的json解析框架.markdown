---
layout: post
title: spring boot 使用别的json解析框架
date: 2019-01-03 10:55:00 +0300
description: spring boot 使用别的json解析框架解析json
img: software.jpg # Add image post (optional)
categories: [spring boot,java]
tags: [spring,java, spring boot] # add tag
---

<font color="red">（注：这个方法真的很白痴，超级不建议看，跳过吧,这篇文章不是最好的方式，可以废弃不读，在后续章节spring boot完美使用Fast Json解析JSON数据，提供更完美的方案。）</font>

spring boot使用fastjson进行json解析，这里有个方案，就是返回数据的时候，不直接返回对象，而是返回string，具体操作如下：
首先，引入fastjson依赖库
```xml
<dependency>
	<groupId>com.alibaba</groupId>
	<artifactId>fastjson</artifactId>
	<version>1.2.7</version>
</dependency>
```
代码修改为：
```java
// 地址：http://localhost:8080/demo/getFastJson
@RequestMapping("/getFastJson")
public String getFastJson(){
	Demo demo=new Demo();
	demo.setId(2);
	demo.setName("zhang san");
	return JSONObject.toJSONString(demo);
}
```
虽然看似多了一行代码，但是使用fastjson对数据的返回的可控性就很强了，后面可能会介绍更好的解决方案。