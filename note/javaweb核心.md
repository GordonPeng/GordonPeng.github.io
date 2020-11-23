# Servlet

## 基本介绍

运行在java服务端的容器，用于接收和响应客户端http请求

三种方式使用servlet：

实现servlet接口

继承HttpServlet

继承GenericServlet



## ServletConfig

servletconfig是servlet初始化配置

## ServletContext

* 一个web只有一个ServletContext  

* 多个servlet数据共享
* web应用加载时创建 停止时销毁

配置：全局初始化参数

```xml
<context-param>
    <param-name>namespace</param-name>
    <param-value>sss</param-value>
</context-param>
```

## @WebServlet 注解

@WebServlet（value=“/aaa”,loadOnStartup=2）



# Request

## 请求行

* 虚拟目录
* 访问者ip
* 请求参数
* URL
* URI
* 映射路径

## header请求头

* 根据头名称获取header
* 

## Parameter请求参数 (请求体)





## 请求域对象 Attribute

请求域 ：只存在于一次请求响应中

请求结束 域对象销毁

## 请求转发

特点：

* 地址不变
* 请求域对象不销毁
* 目的servlet的响应正文丢失



# Response

服务端给客户端的反馈结果



## 响应行

状态码：

* 2**  正常

* 3**

  302: 服务器让浏览器立刻访问另一个地址 重定向

  304: 查找本地缓存  

* 4** 客户端错误

  400: 参数缺失

  401: 无权限访问

  403: 禁止访问

  404: 路径找不到

  405: 不支持访问方式

* 5** 服务端错误

  500: 代码错误

## 响应头

服务器控制浏览器必须设置响应头

* 重定向: "Location"
* 指定编码: "Content-Type" ""
* 文件下载："Content-Disposition"    "attachment;filename=a.jpg"
* 定时刷新："Refresh" "3;URL="

##  响应体

* 字节流
* 字符流

## 定时刷新

setHeader()

## 重定向

特点：

* 可以重定向到其他服务器
* 地址栏改变
* 两次请求 数据不共享



# 中文乱码

## 客户端给服务器提交数据request：

* get：原因 tomcat的编码不是Utf-8,request用Tomcat编译导致

修改：tomcat -->conf-->server.xml--> Connector 8080-->URIEncoding="utf-8"     tomcat8已解决

* post：客户端提交的数据在服务器的request对象中获取时乱码

在request获取数据之前，调用request.setCharacterEncoding("UTF-8");

## 服务端给客户端返回数据response：

原因：从response中默认获取的流默认是西欧编码

解决：重新设置response响应编码response.setCharacterEncoding("UTF-8")

并且控制指定浏览器编码为utf-8：response.setContentType("text/html;charset=utf-8");



# 会话

​	客户端和服务器之间多次的请求和响应 通过会话保存在访问过程中所产生的数据，存在cookie和session中,cookie保存在客户端，session保存在服务端。

## cookie

* 客户端会话管理技术，基于http协议请求头响应头，实现多次请求的数据共享
* cookie携带客户端唯一标识
* 一个cookie是一组键值对
* cookies本质上是一个响应头/请求头
* 可以包含多组键值对,最大4kb，个数最多20（不同浏览器决定）
* 不安全，明文
* 默认会话级，可设置寿命



## session

* session技术是基于cookie实现的
* 在客户端只保存session的ID特殊标识 数据保存在服务器中

getSession():

* 第一次访问 检测cookie有没有带JSESSIONID， 没有创建，有就获取
* 第一次访问 创建：返回发送包含session 的iD的cookie
* 第二次访问 有session不创建session 
* 第二次访问 返回不发送id

关闭浏览器 会话结束 cookie被销毁，再次打开浏览器，由于没有cookie重新创建session。服务端无用session 30分钟后销毁 





# JSP(Java Server Page)

仅用于展示数据，加载前端动态页面

根据请求内容生成其他格式文档的web网页响应给客户端

jsp基于java 本质是Servlet

原理

jsp 翻译成 java代码和html 编译java成class 运行在服务器

3个指令

4个域

九大内置对象

|             |                     |
| ----------- | ------------------- |
| application | ServletContext      |
| request     | HTTPServletRequest  |
| response    | HTTPServletResponse |
| session     | HTTPSession         |
| config      | ServletConfig       |
| exception   |                     |
| page        | this                |
| out         | writer              |
| PageContext |                     |

## PageContext

可以获取其他八个内置对象







# 四大域对象

| 域             | 范围        | 级别 | 备注                |
| -------------- | ----------- | ---- | ------------------- |
| ServletContext | web应用     | **** | web应用被移除时销毁 |
| HttpSession    | 会话        | ***  | 会话结束时销毁      |
| HttpRequest    | 一次请求    | **   | 请求结束销毁        |
| PageContext    | 一个jsp页面 | *    | 页面关闭销毁        |

# MVC

model：数据模型      例如数据库

View：视图                 例如网页

Controller：控制器   例如Servlet





# EL表达式 Expression Language

在JSP页面中获取数据，让我们脱离java代码块和jsp

${域对象的key}

获取基本数据类型、自定义类、数组、list、map

无空指针异常 无索引越界异常 无字符串拼接

逻辑运算符

* ${empty key} 结果返回boolean

域对象显示优先级：以小范围为准

在el表达式中pagecontext可以获取jsp页面其他8个内置对象

eg：${pagecontext.request.contextPath}



# JSTL(java server pages standarded library)

JSP标准标签库（core sql function ...）

1. 导包
2. 添加标签
3. 使用属性

作用：简化JSP中java代码块

~~~ html
<c:forEach var="u" items="${users}">
        <tr>
            <td>${u.username}</td>
            <td>${u.password}</td>
            <td>${u.email}</td>
            <td>${ fn:substring(u.tel, 0, 3) }****${ 					fn:substring(u.tel, 7, 11) }</td>
            <td>${u.birthday}</td>
        </tr>
</c:forEach>
~~~



# filter接口

用于控制器拦截处理，执行特定的功能，再由过滤器决定是否交给请求资源

例如；统一处理编码，登录校验 请求分类

生命周期：

* init
* doFilter 过滤
* destroy

配置方式：

* 注解@WebFilter()
* 配置文件

多个过滤器执行顺序：

*  过滤器名的自然排序 （ servlet3.0 后）
* 按照在web.xml中映射配置定义的先后顺序

拦截行为：dispatcher

* 请求REQUEST
* 转发FORWORD
* 错误页面
* INCLUDE
* 

## FilterChain接口

由Servlet提供，不需要实现直接使用，代表过滤器链对象

FilterChain.doFilter() 放行到下一个过滤器，如果没有下一个，放行到Servlet

多个过滤器：迭代调用过滤器链中下一个过滤器放行方法，类似于if嵌套



# Listener接口

八种监听接口

一类：域对象的创建和销毁 (init /destroy)

* ServletRequestListener
* HttpSessionListener 
* **ServletContextListener**

二类：域对象中属性变化(added/removed/replaced)

* ServletRequestAttributeListener
* HttpSessionAttributeListener
* ServletContextAttributeListener

三类：针对HttpSession的会话域绑定和解绑  钝化和活化

* HttpSessionBindingListener

  valueBound

  valueUnBound

* HttpSessionActivationListener

  sessionWillPassivate 钝化

  sessionDidActivate 活化

  

  