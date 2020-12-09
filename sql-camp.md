# sql-camp 导视

## 0. DQL定位

SQL 语言按照功能可以划分成以下的 4 个部分:

- DDL，英文叫做 Data Definition Language，也就是数据定义语言，它用来定义我们的数据库对象，包括数据库、数据表和列。通过使用 DDL，我们可以创建，删除和修改数据库和表结构。
- DML，英文叫做 Data Manipulation Language，数据操作语言，我们用它操作和数据库相关的记录，比如增加、删除、修改数据表中的记录。
- DCL，英文叫做 Data Control Language，数据控制语言，我们用它来定义访问权限和安全级别。
- DQL，英文叫做 Data Query Language，数据查询语言，我们用它查询想要的记录，它是 SQL 语言的重中之重。在实际的业务中，我们绝大多数情况下都是在和查询打交道，因此学会编写正确且高效的查询语句，是学习的重点。

摘录自【SQL必知必会】

---

- DQL是 SQL的一部分
- SQL 是访问关系型数据库的标准语言
- 数据库指的是数据库管理系统，关系型数据库管理系统分为很多种
- ... 可以学的还很多，DQL只是数据库开发的小小一部分。

## 1. sqlplus 与 IDE

### sqlplus

#### 连接

- 连接远程数据库
- 断开
- 退出

#### 常用指令

- 查看表结构
- 编写sql

  - rowid 与 rownum

- 命令

  - 编辑sql语句
  - 文件操作
  - 格式命令

### IDE

> 集成开发环境。
> 即：
> Integrated Development Environment 
> 一般囊括：编辑器、编译器、调试器、图形界面工具。

#### oracle sql developer

> oracle 自家发行的工具

- [SQL Developer 20.2 Downloads](https://www.oracle.com/tools/downloads/sqldev-downloads.html)

  [^说明]: 需要账号登陆下载

#### pl/sql developer

> 第三方强大ide
> 终端只支持 win
> 只为oracle 而生

- https://www.allroundautomations.com/

- 配置
- 不同窗口

#### Toad（大青蛙）

> 特别棒（据说）的第三方工具，专注于oracle 管理。
> 要钱，且对盗用版本打击极严

#### DataGrip

> Jetbrains 公司旗下产品，要钱的，有30天试用期。功能还行，支持的数据库多。

- [DataGrip 下载](https://www.jetbrains.com/datagrip/)

#### DBeaver

> 开源软件，好处免费，支持终端多，有一些常用的功能。

- [DBeaver 下载](https://dbeaver.io/download/)

## 3. DQL

>  DQL，英文叫做 Data Query Language，数据查询语言，用来查询想要的记录，是 SQL 语言中的重要组成部分。在实际的工作中，绝大多数情况下都在和查询打交道，因此学会编写正确且高效的查询语句，是重中之重

### 书写顺序

- select ... from ... join on ... where ... group by ... having ... order by ... limit

### 执行顺序

- from ... join on ... where ... group by ... having ... select ... order by ... limit

### 表及表间关联from / join

#### from 子句

#### join 

- 内连接 inner join 

  - 也叫等值连接

- 自连接
- 自然连接
- 外连接

  - 左外连接
  - 右外连接

- 全连接

### 选取内容 select

#### 字段名称

##### 函数

- 单行函数

  - 数值函数
  - 字符串函数
  - 日期函数
  - 类型转换函数
  - 其他

    - 字符集转换
    - 条件判断

- 聚合函数
- 分析函数

  - listagg
  - lag
  - lead
  - rank
  - dense_rank
  - row_number
  - first_value
  - last_value
  - ...

### 分组展示 group by

#### having 子句

#### CUBE

#### ROLLUP

### 限制条件及顺序呈现

#### where 子句

- 匹配值

  - like 、 not like
  - in 、 not in
  - is null 、is not null
  - is nan、is not nan
  - between ... and ...

- 比较值

  - =
  - <> or !=
  - <、>、<=、>=
  - ANY
  - SOME
  - ALL

- ...

#### order by 排序

- asc / desc
- nulls first/ nulls last
- ...

### 高级查询

#### 集合操作

#### 层次查询

### 表达式

#### 分析函数

#### group by 子句



## 4. pl/sql 编程

