# SQL*Plus

## 连接说明

> 仅win环境，macOS 尚不确定可行性，但下载对应instant client之后，应该可以使用 SQL*Plus

1. 若本机未安装oracle 保证本机有客户端 package:
   - [oracle官网下载 instant client](https://www.oracle.com/database/technologies/instant-client/downloads.html) 注：从oracle官网下载，需注册用户并登录
   - 按本机对应操作系统及需连接的oracle系统版本下载相应包，至少需下载 Basic Package, ODBC Package , SQL*Plus Package 三个包
   - 一般连接行里的数据库 oracle版本为 12.2 的包足够了，客户端包的版本是向下兼容的，即：12.2兼容11，19.9 兼容 18、12、11...
   - 未避免出现不方便下载的情况，已将12.2.0.1版本的三个包放置在训练营钉盘的【软件工具】中

2. 解压、配置：

   - 下载package 到本地后，解压三个包，并将其解压内容放在同一个文件夹内。

   - 编辑名为 `tnsnames.ora` 的文件，在其末尾添加：

     ```
     CUST =
       (DESCRIPTION =
         (ADDRESS = (PROTOCOL = TCP)(HOST = 【数据库ip】)(PORT = 【数据库端口号】))
         (CONNECT_DATA =
           (SERVER = DEDICATED)
           (SERVICE_NAME = 【数据库实例名】)
         )
       )
     ```

     将上述描述性文字改成数据库实际的ip、端口和实例，例如，你的数据库 ip 为10.100.3.42，端口为1521，实例名为orcl，则应添加如下一段：

     ```
     CUST =
       (DESCRIPTION =
         (ADDRESS = (PROTOCOL = TCP)(HOST = 10.100.3.42)(PORT = 1521))
         (CONNECT_DATA =
           (SERVER = DEDICATED)
           (SERVICE_NAME = orcl)
         )
       )
     ```

3. 好了，现在打开你本机的终端，win 用 `cmd` 或者`powershell` 或者 你用的顺手的其他CIL . mac 也一样，用 `terminal` 或者你下载的用的顺手的其他CIL。输入 `sqlplus` 回车：

   ```
   C:\Users\admin>sqlplus
   
   SQL*Plus: Release 12.2.0.1.0 Production on Sun Dec 13 11:32:30 2020
   
   Copyright (c) 1982, 2016, Oracle.  All rights reserved.
   
   Enter user-name:
   ```

   你会看到如上信息，提示你输入用户名、密码，正确登录后，即可开始使用SQL*Plus

## 操作方式&常用命令

### 一、连接

- 按照 **连接说明** 的描述对远程数据库进行连接。
- 使用 `DISCONNECT` 命令断开数据库连接，使用 `CONNECT` 命令重新连接
- 退出时，可输入 `exit` 或者 `quit` 退出 SQL*Plus

### 二、常用指令

#### 2.1 查看表结构

- 使用 `DESCRIBE` 查看表结构
- 
- 



## reference

- [ORACLE 官方SQL*Plus QuickStart](https://docs.oracle.com/cd/B19306_01/server.102/b14357/qstart.htm)
- [ORACLE 官方介绍](https://docs.oracle.com/en/database/oracle/oracle-database/21/sqpug/SQL-Plus-user-interface.html#)

```css
- 
```

