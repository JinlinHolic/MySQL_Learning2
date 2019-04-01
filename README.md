# MySQL_Learning2

##  导入示例数据库 

根据大大给的教程链接 完成了一次数据库导入 也就是导入到现有的mySQL之中 教程链接再贴一下: https://www.yiibai.com/mysql/how-to-load-sample-database-into-mysql-database-server.html 导入结果如下图所示。

![WeChat Image_20190401204512](https://user-images.githubusercontent.com/43989688/55352505-4a17b600-54c1-11e9-97c4-26d7c61918c9.png)



      

## 最纠结的来了  SQL是什么？MySQL是什么？  

SQL，指结构化查询语言，全称是 Structured Query Language;SQL 可以访问和处理数据库;SQL 是一种 ANSI（American National Standards Institute 美国国家标准化组织）标准的计算机语言。

MySQL是一种开放源代码的关系型数据库管理系统（RDBMS），使用最常用的数据库管理语言--结构化查询语言（SQL）进行数据库管理;MySQL是开放源代码的，因此任何人都可以在General Public License的许可下下载并根据个性化的需要对其进行修改。

## 查询语句 SELECT FROM 
SELECT 要查询的列名 FROM 表名字 WHERE 限制条件; (注意：如果要查询表的所有内容，则把要查询的列名 用一个星号 * 号表示，代表要查询表中所有的列。大多数情况，只需要查看某个表的指定的列。

举例: 从employee表中选择name、age列


       SELECT name,age FROM employee;
       
### 去重查询(distinct)

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

### CASE...END判断语句 (基础操作)

Case具有两种格式。简单Case函数和Case搜索函数。 
--简单Case函数 
CASE sex 
         WHEN '1' THEN '男' 
         WHEN '2' THEN '女' 
ELSE '其他' END 
--Case搜索函数 
CASE WHEN sex = '1' THEN '男' 
         WHEN sex = '2' THEN '女' 
ELSE '其他' END 

## 筛选语句 WHERE 

数据库表一般包含大量的数据，很少需要检索表中的所有行。通常只会根据特定操作或报告的需要提取表数据的子集。只检索所需数据需要指定搜索条件（search criteria），搜索条件也称为过滤条件（filter condition）。在SELECT语句中，数据根据WHERE子句中指定的搜索条件进行过滤。WHERE子句在表名（FROM子句）之后给出 比如:

SELECT prod_name, prod_price
FROM Products
WHERE prod_price = 3.49;

所得结果是 prod_name prod_price


### 运算符/通配符/操作符 参考链接如下:
https://blog.csdn.net/haibo0668/article/details/52539880

##  分组语句 GROUP BY

(1) group by的含义:将查询结果按照1个或多个字段进行分组，字段值相同的为一组
(2) group by可用于单个字段分组，也可用于多个字段分组

select * from employee;
+------+------+--------+------+------+-------------+
| num  | d_id | name   | age  | sex  | homeaddr    |
+------+------+--------+------+------+-------------+
|    1 | 1001 | 张三   |   26 | 男   | beijinghdq  |
|    2 | 1002 | 李四   |   24 | 女   | beijingcpq  |
|    3 | 1003 | 王五   |   25 | 男   | changshaylq |
|    4 | 1004 | Aric   |   15 | 男   | England     |
+------+------+--------+------+------+-------------+

select * from employee group by d_id,sex;

select * from employee group by sex;
+------+------+--------+------+------+------------+
| num  | d_id | name   | age  | sex  | homeaddr   |
+------+------+--------+------+------+------------+
|    2 | 1002 | 李四   |   24 | 女   | beijingcpq |
|    1 | 1001 | 张三   |   26 | 男   | beijinghdq |
+------+------+--------+------+------+------------+
根据sex字段来分组，sex字段的全部值只有两个('男'和'女')，所以分为了两组
当group by单独使用时，只显示出每组的第一条记录
所以group by单独使用时的实际意义不大

参考链接:https://www.cnblogs.com/snsdzjlz320/p/5738226.html

###   HAVING子句

(1) having 条件表达式：用来分组查询后指定一些条件来输出查询结果
(2) having作用和where一样，但having只能用于group by

select sex,count(sex) from employee group by sex having count(sex)>2;
+------+------------+
| sex  | count(sex) |
+------+------------+
| 男   |          3 |
+------+------------+



