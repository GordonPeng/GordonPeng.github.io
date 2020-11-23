# JDBC

java DataBase Connectivity ：执行SQL语句的java API接口规范

* DriverManager  驱动管理对象

  管理驱动

  获取连接对象

* Connection 数据库连接

  获取执行者对象

  管理事务

* Statement   SQL执行者对象

  executeUpdate 	增删改  返回int

  executeQuery       查          返回ResultSet

* ResultSet     查询结果集

  next 判断结果集是否还有数据

  getXXX 获取一行的列数据

