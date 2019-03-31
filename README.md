# MySQL_Learning2

##  导入示例数据库 

根据大大给的教程链接 完成了一次数据库导入 也就是导入到现有的mySQL之中 教程链接再贴一下: https://www.yiibai.com/mysql/how-to-load-sample-database-into-mysql-database-server.html

## 最纠结的来了  SQL是什么？MySQL是什么？  

SQL，指结构化查询语言，全称是 Structured Query Language;SQL 可以访问和处理数据库;SQL 是一种 ANSI（American National Standards Institute 美国国家标准化组织）标准的计算机语言。

MySQL是一种开放源代码的关系型数据库管理系统（RDBMS），使用最常用的数据库管理语言--结构化查询语言（SQL）进行数据库管理;MySQL是开放源代码的，因此任何人都可以在General Public License的许可下下载并根据个性化的需要对其进行修改。

## 查询语句 SELECT FROM 
SELECT 要查询的列名 FROM 表名字 WHERE 限制条件; (注意：如果要查询表的所有内容，则把要查询的列名 用一个星号 * 号表示，代表要查询表中所有的列。大多数情况，只需要查看某个表的指定的列。

举例: 从employee表中选择name、age列


       SELECT name,age FROM employee;
       
## 去重查询(distinct)

在表中，可能会包含重复值。这并不成问题，不过，有时也许希望仅仅列出不同（distinct）的值。关键词 distinct用于返回唯一不同的值。

### 1.作用于单列

举例: 列表A和列表B 





