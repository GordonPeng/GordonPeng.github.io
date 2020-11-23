# Spring

分层的JavaSE/EE full-stack 轻量级应用开源框架

粗粒度封装

核心容器：

* Beans
* Core
* Context
* SpringEI表达式

中间层

* AOP
* Aspects
* Messaging
* Instrumentation
* 。。。

应用层

* web集成
* web实现
* 数据库访问
* 。。。

测试

## IOC

耦合与内聚

* 耦合：代码书写过程中技术结合的紧密度，衡量各个模块之间的互联程度
* 内聚：代码书写过程中单个模块各组成成分之间的联系，衡量模块内部成分之间的联系

追求：高内聚 低耦合

Spring产生背景：为了解决代码与资源之间的高耦合，采用工厂模式管理创建资源，利用配置文件注册资源，从而化解代码与资源之间的高耦合，转嫁到配置文件与资源的耦合，由于配置文件只需要读取，不需要编译运行，修改维护方便，从而解决高耦合问题

控制翻转：Spring 反向控制应用程序需要的资源，主动管理变被动接收

IOC容器：Spring 控制的资源全部放到Spring容器中，称之为IOC容器



## Bean配置

**定义资源属性**

name： 别名 通过name获取bean

id：bean的名称 通过id获取bean 

class：包名.类名

scope：

* singleton：单例
* propotype：非单例 默认 

**生命周期**

init() 创建时调用

destroy()销毁时调用 非单例模式不被spring容器管理

**DI(依赖注入)**     Dependency Injection

* set

  声明私有变量

  提供set方法

  将要注入的资源声明为bean交给容器控制

  ~~~xml
  <bean id="aa" class="..."/>
  ~~~

  注入

  ~~~xml
  <bean id=>
      <property name="" ref=""></property>
  </bean>
  ~~~

  

* 构造方法注入

  

