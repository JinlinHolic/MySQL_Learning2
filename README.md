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

举例: 列表A有两列 分别是id和name  


        select distinct name from A
        
出来结果只是仅仅列出不同的id和与之匹配的唯一不重复name

###  前N个语句

SELECT * FROM table LIMIT [offset,] rows | rows OFFSET offset
LIMIT 子句可以被用于强制 SELECT 语句返回指定的记录数。LIMIT 接受一个或两个数字参数。参数必须是一个整数常量。
如果给定两个参数，第一个参数指定第一个返回记录行的偏移量，第二个参数指定返回记录行的最大数目。
初始记录行的偏移量是 0(而不是 1)： 为了与 PostgreSQL 兼容，MySQL 也支持句法： LIMIT # OFFSET #。
mysql> SELECT * FROM table LIMIT 5,10; // 检索记录行 6-15 ,注意，10为偏移量 
//为了检索从某一个偏移量到记录集的结束所有的记录行，可以指定第二个参数为 -1：
mysql> SELECT * FROM table LIMIT 95,-1; // 检索记录行 96-last.
//如果只给定一个参数，它表示返回最大的记录行数目：
mysql> SELECT * FROM table LIMIT 5; //检索前 5 个记录行 //也就是说，LIMIT n 等价于 LIMIT 0,n。
如果你想得到最后几条数据可以多加个 order by id desc

mysql不支持select top n的语法，应该用这个替换：
select * from tablename order by orderfield desc/asc limit position， counter；
position 指示从哪里开始查询，如果是0则是从头开始，counter 表示查询的个数
取前15条记录：
select * from tablename order by orderfield desc/asc limit 0,15

### CASE...END判断语句







