---
layout: post
title: spring boot 全局异常捕捉
date: 2019-01-04 10:15:00 +0300
description: spring boot 统一异常处理方案
img: software.jpg # Add image post (optional)
categories: [spring boot,java]
tags: [spring,java, spring boot] # add tag
---
在一个项目中的异常，我们通常都会统一进行处理，下面就介绍如何进行统一处理。

首先，新建一个类<font color="blue">GlobalDefaultExceptionHandler</font>，在class注解上@controllerAdvice，在方法上注解@ExceptionHandler(Value=Exception.class),具体代码如下：
```Java
package com.example.demo.exception;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.servlet.ModelAndView;

import javax.servlet.http.HttpServletRequest;

@ControllerAdvice
public class GlobalDefaultExceptionHandler {
    private final static Logger logger= LoggerFactory.getLogger(GlobalDefaultExceptionHandler.class);

    /**
     * 增加注解ExceptionHandler，注解ExceptionHandler中value的值是要处理的异常类，
     * 返回json数据或者String数据需要在方法上加上注解 @ResponseBody
     * 返回视图，定义一个ModelAndView即可，然后return；定义视图文件（如：error.html,error.ftl,error.jsp）
     * @param request
     * @param e
     * @return 返回值String
     */
    @ExceptionHandler(value = ArithmeticException.class)
    @ResponseBody
    public String defaultErrorHandler(HttpServletRequest request,Exception e){
        logger.info("全局错误捕捉url:"+request.getRequestURI());
        logger.error(e.getMessage(),e);
        return "url:"+request.getRequestURI()+"数据运算错误："+e.getMessage();
    }

    /**
     * 统一处理错误返回视图
     * @param request
     * @param e
     * @return
     */
    @ExceptionHandler(value = Exception.class)
    public ModelAndView errorHandler(HttpServletRequest request, Exception e){
        logger.info("全局错误捕捉url:"+request.getRequestURI());
        logger.error(e.getMessage(),e);
        ModelAndView modelAndView=new ModelAndView();
        modelAndView.addObject("exception", e);
        modelAndView.addObject("url", request.getRequestURL());
        modelAndView.setViewName("error");
        return modelAndView;
    }
}
```
在ExceptionController中加入方法
```java
package com.example.demo.controller;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/exception")
public class ExceptionController {

    @RequestMapping("/zeroException")
    public int zeroException(){
        return 100/0;
    }
}
```
访问：http://localhost:8080/exception/zeroException这个方法肯定是抛出异常的，那么在控制台就可以看到我们全局捕捉的异常信息了。更精确的异常捕捉就是把每个异常都单独的写一个处理方法，就好比上面GlobalDefaultExceptionHandler类中的defaultErrorHandler，只会处理ArithmeticException，errorHandler方法会处理所有的异常