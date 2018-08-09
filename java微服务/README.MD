# spring boot 初体验

## 简介

* 需要关注点：了解技术体系
  * 技术历史
  * 技术发展脉络
  * 技术思想
  * 技术演变过程
* SUN java认证
  * SCJP
  * SCWSD
  * SCBCD
  * Oracle OCA

## 问题



## 误区



## 我的观点



## 小马哥观点

尽信书则不如无书

三层编码能力，七层分析解决能力

Spring是基础

Java是基础

网上的讲法可能片面，要客观去看待



## 微服务的介绍

###### 概念

> Microservices are a more concrete and modern interpretation of service-oriented architectures (SOA) used to build distributed software systems（Source:wikipedia）
>
> 微服务是用于构建**分布式软件系统**（源：wikipedia）的面向服务架构（SOA）的更具体和现代的解释。



###### 单体应用

>单体应用  VS  微服务
>
>* 优势
>  * 开发
>  * 稳定
>  * 性能
>  * 部署
>* 不足
>  * 中心化 centralization
>  * 耦合 coupling     
>  * 学习成本 learning cost
>  * 伸缩 scale
>  * 持续交付 continuous delivery



###### SOA

![1533534411149](C:\Users\boyuan\AppData\Local\Temp\1533534411149.png)

>SOA    VS   微服务
>
>* 类同
>  * 面向服务  service-oriented
>  * 松耦合 loose-coupling
>  * 模块化 modular
>  * 分布式计算 distributed computing
>  * 平台无关性 independent platform
>* 差异
>  * 原子性   atomic
>  * 领域驱动设计  ddd
>  * 开发运维体系 devops



代码结构   分层

工程结构   模块化

系统层面   服务拆分

微服务是老的概念翻出来炒一下

应用规模、从实际出发 --> 合适的架构   微服务还是非微服务



## 微服务发展的历程

###### 分布式计算模型

* 模型
  * 客户端-服务端（Client-Server）
  * 点对点（Peer To Peer
* 分类
  * 同步
  * 异步
* 通讯协议
  * HTTP
  * 自定义协议
* 传输介质
  * 文本 (二进制上加上编码)
  * 二进制

###### SOA

* 层次划分
  * 消费接口
  * 业务处理
  * 服务组件
* 技术
  * SOAP
  * CORBA   比较旧的，80年代
  * RMI
  * REST   2000年的论文
  * ESB



## 微服务面临的挑战

- 技术挑战

  - 注册与发现（Registry and Discovery）

  - 路由（Routing）

  - 可靠性（ Reliability ）

  - 延迟（Latency ）   

    网络延迟   序列化与反序列化

  - 热点（Hotspot）  

    

  - 短路（ Circuit Break ）

    保护

  - 伸缩（Scale）

  - 异步（Async）

    spring5中，reactive 异步事件驱动

  - 监控（Monitoring）

  - 配置（Configuration）

  - 数据同步（Data Sync）

    比较大的挑战  CAP

    数据：水平分、垂直分、业务分、区域分

  - 安全（Security）

    web前端安全  XSS

    权限

    服务与服务之间是否有权限  单点登录、第三方登录



## JAVA微服务实战

* 元编程（Meta Programming）

  在Java编程语言中，元编程是一种新型的编程模式，目的是减少代码行数，得到事半功倍的效果。

  * 主要模式

    * 注解驱动（Annotation-Driven）
    * 反射驱动（Reflection-Driven）
    * 表达式驱动（Expression-Driven）
    * Lambda（Java 8 Introduced）
    * Script On JVM（Groovy、JavaScript等） 

  * 接口编程（Interface Programming）

    又称之为契约编程，在OOP语言中，其契约范围包括方法名称、方法入参（类型和顺序）、方法返回值（类型）以及异常情况等元数据。



spring-boot-starter-actuator



Endpoints

使用的场景和逻辑思维







# spring boot web篇（上）

静态内容：简介传统 Web Server，Java Web Server 以及 Spring Boot 处理静态内容。

动态内容：介绍传统 Servlet 容器以及 Spring Boot 处理是如何处理动态内容。

模板引擎：介绍老、中、新三代模板引擎（传统 JSP ，中生代 Velocity、以及后现代 Thymeleaf）发展过程，Spring Boot 使用方法，以及三者的特征优劣。



* 计算类型
  * I/O密集型 
    * socket连接  文件传输
  * CPU密集型
    * 算法，比如很大的数组中找一个值
  * 内存密集型 
    * cache

## 静态web内容

* 常见静态Web内容
  * HTML
  * CSS
  * JS
  * JPEG
  * Flash
  * ...
* 计算类型
  * I/O类型
    * SOCKET io    必须要有服务器地址和端口
    * 进程类IO   内存  外存
* 交互方式
  * 单一
* 资源内容
  * 基本相同
* 资源路径
  * 物理路径（文件、目录）
* 请求方法
  * GET(主要)
* 常见使用场景
  * 信息展示
  * 样式文件（CSS）
  * 脚本文件（JS）
  * 图片（JPEG、GIF）
  * 多媒体库（Flash、Movie）
  * 文件下载
* 常见web服务器
  * Apache Http Server     http://www.apache.org
  * Nginx     http://nginx.org/
  * Microsoft IIS
  * GWS    （google）
* 思考
  * 为什么Java Web Server不是常用Web Server？
    * 内存占用
      * 类型
      * 分配
    * 垃圾回收
      - 被动回收
      - 停顿
    * 并发处理    
      - 线程池
      - 线程开销  poxis
* 标准优化技术
  * 资源变化
    * 响应头    Last-Modified
    * 请求头    If-Modified-Since
  * 资源缓存
    * 响应头	ETag
    * 请求头     If-None-Match



动静分离

## 动态web内容

* 常见动态web内容
  * 
* 计算类型
  * 混合类型
* 交互方式
  * 用户输入
  * 客户端特征
  * ...
* 资源内容
  * 多样性
* 资源路径
  * 逻辑路径（虚拟）
* 请求方法
  * GET
  * POST
  * HEAD
  * PUT
* 常用场景
  * 页面渲染
  * 表单交互（Form）
  * AJAX
  * XML
  * JSON/JSONP
  * Web Services（SOAP、WSDL）
  * WebSocket
* 流行Java Web 服务器
  * Servlet容器（Tomcat、Jetty）
  * 非Servlet容器（Undertow）
* 请求
  * 资源定位 （URI）
  * 请求协议（Protocol）
    * http
    * https
  * 请求方法（Method）
  * 请求参数（Parameter）
  * 请求主体（Body）
  * 请求头（Header）
  * Cookie
* 响应
* 技术/架构演变
  * CGI (Common Gateway Interface)
  * Servlet 
  * JSP (Java Server Page)
  * Model1 (JSP + Servlet  + JavaBeans)  
    * javaBeabs
      * EJB
      * 普通pojo
  * Model2 (MVC)



## 模板引擎

* JSP
  * 
* Velocity   
  * apache
  * spring 整合velocity
  * Spring4.3 之后，不再被spring支持
  * Spring Boot 1.5.x不再支持Velocity
    * Velocity   Engine1.7版本发布时间  2010-11-20
    * 用freemark替代
* Thymeleaf
  * ThymeleafProperties



@ConfigurationProperties

spring boot查看源码

* xxxProperties 





## 问答互动









# spring boot web篇（中）

对spring boot 和spring cloud基础还是在对spring的了解



## REST理论基础

* 基本概念
* 历史
  * REST来自于Roy Thomas Fielding 2000年的博士论文  <Architectural Styles and the Design of Network-based Software Architectures >
* 类似形式
  * Web Services
  * WSDL
  * SOAP
* 架构属性
  * 性能（Performance）
  * 可伸缩性（Scalability）
  * 统一接口简化性（Simplicity of a uniform Interface）
  * 组件可修改性（Modifiability of components）
  * 组件通讯可见性（Visibility of communication between components）
  * 组件可移植性（Protability of component）
  * 可靠性（Reliability）
* 架构约束
  * C/S架构（client-server）
  * 无状态（stateless）
  * 可缓存（cacheable）
    * Etag 
    * 主要是服务端缓存
    * 
  * 分层系统（layered system）
    * 
  * 按需代码（code on demand）
    * 
  * **统一接口**（uniform interface）   重点
    * 资源识别（Identification of resources）
      * URI： Uniform Resource Identifier
    * 资源操作（Manipulation  of resources through representations）
      * HTTP verbs：GET、PUT、DELETE、POST
    * 自描述消息（Self-descriptive messages）
      * Content-Type
      * MIME-Type
      * Media Type
    * 超媒体（HATEOAS）
      * Hypermedia As The Engine Of Application State



## REST服务端实践

* Spring Boot REST

  * 核心接口
    * 定义相关
      * @Controller
      * @RestController
        * @Controller
        * @ResponseBody
    * 映射相关
      * @RequestMapping
      * @PathVariable
    * 请求相关
      * @RequestParam
      * @RequestHeader
      * @CookieValue
      * RequestEntity
    * 响应相关
      * @ResponseBody
      * ResponseEntity

* HATEOAS

  ```java
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.beans.factory.annotation.Qualifier;
  import org.springframework.context.annotation.Bean;
  import org.springframework.http.MediaType;
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.PostMapping;
  import org.springframework.web.bind.annotation.RequestParam;
  import org.springframework.web.bind.annotation.RestController;
  
  import static org.springframework.hateoas.mvc.ControllerLinkBuilder.linkTo;
  import static org.springframework.hateoas.mvc.ControllerLinkBuilder.methodOn;
  
  @RestController
  public class JSONRestController {
  
      @Bean
      public User currentUser() {
          User user = new User();
          user.setName("JSON");
          user.setAge(20);
          return user;
      }
  
      @Autowired
      @Qualifier("currentUser")
      private User user;
  
      @GetMapping(path = "/json/user",
              produces = MediaType.APPLICATION_JSON_VALUE)
      public User user() {     user.add(linkTo(methodOn(JSONRestController.class).setUserName(user.getName())).withSelfRel());
    user.add(linkTo(methodOn(JSONRestController.class).setUserAge(user.getAge())).withSelfRel());
          return user;
      }
  
      //setName
      @PostMapping(path = "/json/user/set/name",
              produces = MediaType.APPLICATION_JSON_VALUE)
      public User setUserName(@RequestParam String name) {
          user.setName(name);
          return user;
      }
  
      //setAge
      @GetMapping(path = "/json/user/set/age",
              produces = MediaType.APPLICATION_JSON_VALUE)
      public User setUserAge(@RequestParam int age) {
          user.setAge(age);
          return user;
      }
  }
  
  ```

  

* REST文档生成

  * Spring boot /mappings endpoint
  * spring RestDocs
  * swagger



## REST客户端实践

* Web 浏览器
* 
* Spring RestTemplate



## 问答互动

hsf





# spring boot web篇（下）

## 传统 Servlet 回顾

* 什么是Servlet？

  > Servlet 是一种基于 Java 技术的 Web 组件，用于生成动态内容，由容器管理。类似于其他 Java 技术组件，Servlet 是平台无关的 Java 类组成，并且由 Java Web 服务器加载执行。

* 什么是Servlet容器？	

  > Servlet 容器，有时候也称作为 Servlet 引擎，作为Web服务器或应用服务器的一部分。通过请求和响应对话，提供 Web 客户端与 Servlets 交互的能力。容器管理Servlets实例以及它们的生命周期。

* 历史

  > 1997年六月，Servlet 1.0 版本发行，最新版本 Servlet 4.0 处于研发状态。

* 核心接口

  * Servlet 3.0前时代
    * 服务组件
      * javax.servlet.Servlet
      * javax.servlet.Filter (since Servlet 2.3)
    * 上下文组件
      * javax.servlet.ServletContext
      * javax.servlet.http.HttpSession
      * javax.servlet.http.HttpServletRequest
      * javax.servlet.http.HttpServletReponse
      * javax.servlet.http.Cookie (客户端)
    * 配置
      * javax.servlet.ServletConfig
      * javax.servlet.FilterConfig (since Servlet 2.3)
    * 输入输出
      * javax.servlet.ServletInputStream
      * javax.servlet.ServletOutputStream
    * 异常
      * javax.servlet.ServletException
    * 事件  (since Servlet 2.3)
      * 生命周期类型
        * javax.servlet.ServletContextEvent
        * javax.servlet.http.HttpSessionEvent
        * javax.servlet.ServletRequestEvent
      * 属性上下文类型
        * javax.servlet.ServletContextAttributeEvent
        * javax.servlet.http.HttpSessionBindingEvent
        * javax.servlet.ServletRequestAttributeEvent
    * 监听器  (since Servlet 2.3)
      * 生命周期类型
        * javax.servlet.ServletContextListener
        * javax.servlet.http.HttpSessionListener
        * javax.servlet.http.HttpSessionActivationListener
      * 属性上下文类型
        - javax.servlet.ServletContextAttributeListener
        - javax.servlet.http.HttpSessionAttributeListener
        - javax.servlet.http.HttpSessionBindingListener
        - javax.servlet.ServletRequestAttributeListener
  * Servlet 3.0 后时代
    * 组件申明注解
      * @javax.servlet.annotation.WebServlet
      * @javax.servlet.annotation.WebFilter
      * @javax.servlet.annotation.WebListener
      * @javax.servlet.annotation.WebSecurity
      * @javax.servlet.annotation.HttpMethodConstraint
      * @javax.servlet.annotation.HttpConstraint
    * 配置申明
      * @javax.servlet.annotation.WebInitParam
    * 上下文
      * javax.servlet.AsyncContext
    * 事件
      * javax.servlet.AsyncEvent
    * 监听器
      * javax.servlet.AsyncListener
    * Servlet 组件注册
      * javax.servlet.ServletContext#addServlet()
      * javax.servlet.ServletRegistrationFilter
    *  组件注册
      * javax.servlet.ServletContext#addFilter()
      * javax.servlet.FilterRegistration
    * 监听器注册
      * javax.servlet.ServletContext#addListener()
      * javax.servlet.AsyncListener

## Servlet on Spring Boot 



## JSP on Spring Boot



## 问答互动 

