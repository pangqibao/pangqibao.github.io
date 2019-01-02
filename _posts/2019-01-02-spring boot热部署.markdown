---
layout: post
title: spring boot 热部署
date: 2019-01-02 11:32:00 +0300
description: spring boot 热部署，coding完项目快速生效
img: software.jpg # Add image post (optional)
categories: [spring boot,java]
tags: [spring,java, spring boot] # add tag
---
### Spring Boot热部署
  编写代码的适合，你会发现我们只是简单的改变了一下打印信息，就需要重新部署，如果这样的编码方式，那么我们估计一天下来就只能在打印和部署之间徘徊，一天下来写不了几个代码了，spring boot提供了一个热部署的工具，即springloaded，加入如下配置
  ```xml
  <plugin>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-maven-plugin</artifactId>
	<dependencies>
		<!--springloaded  hot deploy --> 
		<dependency> 
			<groupId>org.springframework</groupId> 
			<artifactId>springloaded</artifactId> 
			<version>1.2.4.RELEASE</version>
		</dependency> 
    </dependencies> 
    <executions> 
        <execution> 
            <goals> 
                <goal>repackage</goal> 
            </goals> 
            <configuration> 
                <classifier>exec</classifier> 
            </configuration> 
        </execution> 
    </executions>
  </plugin>
  ```
如果是使用spring-boot:run的话，那么到此配置结束，现在就可以体验coding的爽了
如果使用的是run as - appliation的话，那么还需要一些处理
把spring-loader-1.2.4.RELEASE.jar下载下来，放到项目目录lib中，然后把idea的run参数VM设置为
> -javaagent:.\lib\springloaded-1.2.4.RELEASE.jar -noverify

然后启动就可以了，这样在run as 的时候，也能进行热部署了。
当然不是所有的代码都支持热部署，呃，我也不是很清楚，那些代码修改了可以直接不用重启查看
特别说明：

	> 比较常用的打包命令	
	> mvn clean packagespring-boot:repackage 
	> 只有使用下面的maven命令在cmd窗口启动，热加载才能生效，如果直接run运行的application，是不支持热加载的
	> mvn clean spring-boot:run 
	
	参考：http://blog.csdn.net/z69183787/article/details/46520595 (http://blog.csdn.net/z69183787/article/details/46520595)
	如果使用run 也可以热部署的话，配置vm参数，请查看：http://www.tuicool.com/articles/RvIf2mY (http://www.tuicool.com/articles/RvIf2mY)
