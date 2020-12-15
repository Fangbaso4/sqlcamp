# Simple DQL

---

> 在预习周，《SQL必知必会》中关于单句sql查询和关连查询，有过一个大致的介绍。此处默认大家已经掌握基本的DQL语句，本周将针对句法结构、关连说明、单行函数、限制条件、集合操作进行阐述与训练。
>
> 本部分示例 sql 使用 ORACLE scott 用户数据（12版本往后就没有这个用户了）

句法结构

`select ... from ... join on ... where ... group by ... having ... order by ... `

from / join 部分(`source_list`)

- 单表查询

### 多表查询

- #### 多表关连 `join`

  - 等值连接 `Equijoins`

    

  - 范围连接 `Band Joins`

  - 自连接 `Self Joins`

  - 笛卡尔积 `Cartesian Products`

  - 内连接 `Inner Joins`

  - 外连接 `Outer Joins`

  -  `Antijoins`

  -  `Semijoins`

- #### 子查询 `Subqueries`

  - 相关子查询 `Related Subqueries`
  - 嵌套子查询 `Nested Subqueries`
    - 子查询在  `select`  部分
    - 子查询在  `from`  部分
    - 子查询在  `where`  部分

where 部分



select 部分（`select_list`）

> select_list 可以展开很多，如分析函数、hint 等等，本部分主要介绍一些常用场景下使用的单行函数.
>
> ---待20-12-17更新

## 其他

### 集合操作

- 并集
- 交集
- 差集

### DUAL 表

### dbLink 查询





## Reference

- [官方SQL 参考手册（DQL部分）](https://docs.oracle.com/en/database/oracle/oracle-database/21/sqlrf/SQL-Queries-and-Subqueries.html#GUID-5937EB2B-D3EC-45D4-BF75-1FC02E45DAE2)
- [Live SQL 时间格式化](https://livesql.oracle.com/apex/livesql/file/content_BFKOA5UQHDV1MV7HRUDDUEPM4.html)
- 