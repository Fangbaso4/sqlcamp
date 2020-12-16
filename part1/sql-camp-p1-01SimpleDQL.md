# Simple DQL

---

> 在预习周，《SQL必知必会》中关于单句sql查询和关连查询，有过一个大致的介绍。此处默认大家已经掌握基本的DQL语句，本周将针对句法结构、关连说明、单行函数、限制条件、集合操作进行阐述与训练。
>
> 本部分示例大部分为ORACLE官方示例，相关文章及样例数据将上传至【参考资料】，使用 ORACLE 的OT 库及对应的表和数据，文末附有链接.
>
> 注意：本文表间 join 的大部分SQL示例使用 SQL 99 语法规范，使用其他语法规范部分会特殊标注。

## 句法结构

**书写结构**

`select ... from ... join on ... where ... group by ... having ... order by ... `

**执行顺序**

`from ... join on ... where ... group by ... having ... select ... order by ...`

## from / join 部分(`source_list`)

### 单表查询

 	from 后直接跟表名 表别名 即可， `from table_name table_alias` 。

### 多表查询

- #### 多表关连 `join`

  > 多表关联单纯用文字表述比较晦涩，因为SQL是操作数据集合，所以用数学集合概念中的维恩图来展示会一目了然。图片会尽量附在文中。

  - 等值连接 `Equijoins`

    - 在连接中使用等于操作符(=)

    - 如下

      ```sql
      SELECT last_NAME, job_id, departments.department_id, department_name
      FROM employees, departments
       WHERE employees.department_id = departments.department_id
       ORDER BY last_NAME, job_id;
      ```

  - 范围连接 `Band Joins`

    - 在连接中使用除等号之外的操作符，如：`<、>、BETWEEN` 

    - 如下：

      ```sql
      SELECT  e1.last_name || 
              ' has salary between 100 less and 100 more than ' || 
              e2.last_name AS "SALARY COMPARISON"
      FROM    employees e1, 
              employees e2
      WHERE   e1.salary 
      BETWEEN e2.salary - 100 
      AND     e2.salary + 100;
      ```

  - 自连接 `Self Joins`

    - 使用自连接可以将自身表当作另一个表来对待，从而能够得到一些特殊的数据。

    - 如下：

      ``````sql
      SELECT e1.last_name || ' works for ' || e2.last_name "Employees and Their Managers"
        FROM employees e1, employees e2
       WHERE e1.manager_id = e2.employee_id
         AND e1.last_name LIKE 'R%'
       ORDER BY e1.last_name;
      ``````

  - 笛卡尔积 `Cartesian Products`

    - 当两个表没有连接条件，或者连接条件是实际上不成立的时候，Oracle数据库将返回其笛卡尔积。即，将A表的每一行与B表的每一行结合在一起。笛卡尔积返回行数较多，一般不予使用。

      示例：`select * from t1,t2;`  92语法：`select * from t1 cross join t2`

  - 内连接 `Inner Joins`

    - 两个或多个表连接时，仅返回满足连接条件的行，某种情况下可以实现条件限制的效果。

    - 如下：
  
      ``````sql
      SELECT d1.department_name,e1.*
        FROM employees e1
       INNER JOIN departments d1
        ON e1.manager_id = d1.manager_id;
      ``````

  - 外连接 `Outer Joins`

    - 连接条件中的一列包含空值也会返回一行。
  
    - 如下：
    
      ``````sql
      --sql99 左外连接
      SELECT d.department_id, e.last_name
         FROM departments d
         LEFT JOIN employees e
         ON d.department_id = e.department_id
         ORDER BY d.department_id, e.last_name;
      --sql92 左外连接
      SELECT d.department_id, e.last_name
         FROM departments d, employees e
         WHERE d.department_id = e.department_id(+)
       ORDER BY d.department_id, e.last_name;关于左外连接和右外连接：
      /**左外连接，就是指左边的表是主表，需要显示左边表的全部行，而右侧的表是从表，（+）表示哪个是从表/
      ``````
    - 关于左外连接和右外连接：
      左外连接，就是指左边的表是主表，需要显示左边表的全部行，而右侧的表是从表，SQL92语法中（+）表示哪个是从表；
      
      右外连接，指的就是右边的表是主表，需要显示右边表的全部行，而左侧的表是从表。



  - `Antijoins`

    - 未找到准确译名，可以理解为反连接

    - 如下:

      ``````sql
        SELECT *
           FROM employees
          WHERE department_id NOT IN
                (SELECT department_id FROM departments WHERE location_id = 1700)
          ORDER BY last_name;
      ``````

  - `Semijoins`

    - 未找到准确译名，可理解为半连接或者存在连接：

    - 如下：

      ``````sql
      SELECT *
          FROM departments
         WHERE EXISTS (SELECT *
                  FROM employees
                 WHERE departments.department_id = employees.department_id
                   AND employees.salary > 2500)
         ORDER BY department_name;
      ``````

      ![sqljoins](E:\GIT\sqlcamp\sql-camp\references\sqljoins.jpg)

- #### 子查询 `Subqueries`

  > 按子查询在的子句部位分成了如下四个类型。但依照子查询与外部查询是否相关，还可以划分为独立子查询、相关子查询  `Related Subqueries` 和 嵌套子查询 `Nested Subqueries` 。示例中会具体说明属于哪种子查询。

  - 子查询在  `select`  部分

    - 如下：其中，第一个子查询 `COMPANY_MAX_SALARY` 为独立子查询， `less_than` 是相关子查询

      ``````sql
      SELECT (SELECT MAX(salary) FROM employees) AS COMPANY_MAX_SALARY,
                E1.JOB_ID,
                E1.salary,
                (SELECT MAX(salary) - e1.salary FROM employees) AS less_than
           FROM employees e1
           LEFT JOIN departments d1
             ON e1.department_id = d1.department_id
          WHERE d1.department_name = 'IT';
      ``````

      

  - 子查询在  `from`  部分（内联视图）

    - 如下：

      ``````sql
      SELECT *
        FROM (SELECT first_name, last_name, JOB_ID
                FROM employees
               WHERE salary < 2500);
  --嵌套子查询：
      SELECT d1.department_name
      FROM (SELECT e1.*
                FROM employees e1
             INNER JOIN (SELECT department_id, COUNT(1) nums
                            FROM employees d
                         GROUP BY department_id) e2
                  ON e1.department_id = e2.department_id
               AND e2.nums > 5
               WHERE e1.salary > 5000) e
        LEFT JOIN departments d1
          ON e.department_id = d1.department_id
       GROUP BY d1.department_name
        ;
      ``````
      
  
  - 子查询在  `where`  部分 
  
    - 类似于 上一部分的 `Antijoins` 和  `Semijoins` ，其中 `Antijoins`  为独立子查询， `Semijoins` 是相关子查询。
  
  - 子查询在 `having` 部分
  
    - 如下：
    
      
    
    

## where 部分

> ---待20-12-17更新



## select 部分（`select_list`）

> select_list 可以展开很多，如分析函数、hint 等等，本部分主要介绍一些常用场景下使用的单行函数以及聚合函数
>
> ---待20-12-17更新

## order by 部分

> --待20-12-17更新
>
> 

## 其他

### 集合操作

> 本营不涉及数组集合等其他数据库对象，仅对数据集合操作的 sql 书写进行介绍。同样的维恩图对于理解SQL的集合操作有很大的帮助。

![sqlunion](E:\GIT\sqlcamp\sql-camp\references\sqlunion.png)

- 并集
  - UNION (带去重)
  
  - UNION ALL（不带去重）
  
    ```sql
    SELECT product_id FROM order_items
    UNION
    SELECT product_id FROM inventories
    ORDER BY product_id;
    
    SELECT location_id FROM locations
    UNION ALL
    SELECT location_id FROM departments
    ORDER BY location_id;
    ```
  
    
  
- 交集

  - INTERSECT

    ```sql
    SELECT product_id FROM inventories
    INTERSECT
    SELECT product_id FROM order_items
    ORDER BY product_id;
    ```

- 差集
  
  - MINUS
  
    ```sql
    SELECT product_id FROM inventories
    MINUS
    SELECT product_id FROM order_items
    ORDER BY product_id;
    ```
  
    

### DUAL 表

oracle 自带的一张内部表，有一个 `DUMMY` 列,同时始终只有一行数据 `x` ，做一些特定查询时用 DUAL 表是很方便的，比如返回现在的系统时间：`select sysdate from dual;`  拿来做计算器： `select 1+1 from dual;` 等等等

### 远程查询

- 跨库查询
  - 若本库与其他远程数据库建立了 dblink  ，在跨库查询时使用 `username.tablename@dblinkname` 作为表名查询
- 跨用户查询（这个不算远程查询，先放这里）
  - 同一个数据库跨用户查询，若有权限可以直接使用 `username.tablename` 作为表名查询





## Reference

- [官方SQL 参考手册（DQL部分）](https://docs.oracle.com/en/database/oracle/oracle-database/21/sqlrf/SQL-Queries-and-Subqueries.html#GUID-5937EB2B-D3EC-45D4-BF75-1FC02E45DAE2)
- [Live SQL 时间格式化](https://livesql.oracle.com/apex/livesql/file/content_BFKOA5UQHDV1MV7HRUDDUEPM4.html)
- [官方样例数据库](https://www.oracletutorial.com/getting-started/oracle-sample-database) 
- 

 