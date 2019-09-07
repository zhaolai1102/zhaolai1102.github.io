---
layout:     post                  #不要管他
title:      从零开始学postgreSQL     #标题
subtitle:   pgsql              #别名,简介,标题下面的那一行字
date:       2019-09-07            #发表时间
author:     Zhaolai                    #作者
header-img: img/post-bg-rwd.jpg   #背景图片
catalog: true                     #导航目录,不要管他
original: true                    #是否原创申明
tags:                             #标签,可以有多个
    - pgsql
    - sql
---
## 安装与使用

安装sudo apt-get install postgresql

登录sudo -u postgres psql

创建库create database 库名;

退出\q

进入指定的数据库sudo -u postgres psql -d 库名

## 数据类型

#### 数字

integer 整数

#### 字符

char 定长字符串

varchar 边长字符串

Oracle 中使用 VARCHAR2 型(Oracle中也有 VARCHAR 这种数据类型,但并不推荐使用)。

#### 日期

date 年月日

Oracle 中使用的 DATE 型还包含时分秒

## 表

#### 修改表结构

增加列

ALTER TABLE < 表名 > ADD COLUMN < 列的定义 > ;

删除列

ALTER TABLE < 表名 > DROP COLUMN < 列名 > ;

#### 插入数据

开始事物

BEGIN TRANSACTION;

插入数据

INSERT INTO Product VALUES('0001', 'T 恤衫 ', ' 衣服 ', 1000, 500, '2009-09-20');

提交

COMMIT;

插入空值写null,默认值写default

插入查询到的值

```sql
INSERT INTO ProductCopy (product_id, product_name, product_type,sale_price, purchase_price, regist_date) 
SELECT product_id, product_name, product_type, sale_price,
purchase_price, regist_date
FROM Product;
```

#### 修改表名

这个差别很大,取决于数据库的作者.

Oracle, PostgreSQL

ALTER TABLE Poduct RENAME TO Product;

DB2

RENAME TABLE Poduct TO Product;

SQL Server

sp_rename 'Poduct', 'Product';

MySQL

RENAME TABLE Poduct to Product;

## 查询数据

#### 去重

select distinct 字段1, 字段2 from 表名

distinct只能用与第一个字段前, null也算一种

#### exists

存在, 

SELECT product_name, sale_price FROM Product AS P WHERE EXISTS 

(SELECT * FROM ShopProduct AS SP WHERE SP.shop_id = '000C' AND SP.product_id = P.product_id);

#### CASE表达式

可以写多个when子句, 当求值表达式为true时, 执行then 表达式, 当所有的都为false时, 执行else 表达式, end不可以少, 因此只返回一个表达式即一个值,可以用来求和...

case when 求值表达式 then 表达式

else 表达式

end

```sql
搜素CASE表达式
SELECT product_name,
CASE WHEN product_type = ' 衣服 ' THEN 'A : ' | | product_type
WHEN product_type = '办公用品 ' THEN 'B : ' | | product_type
WHEN product_type = '厨房用具' THEN 'C : ' | | product_type
ELSE NULL
END AS abc_product_type
FROM Product;
```

```sql
简单CASE表达式
SELECT product_name,
CASE product_type
WHEN ' 衣服 ' THEN 'A : ' | | product_type
WHEN ' 办公用品' THEN 'B : ' | | product_type
WHEN ' 厨房用具 ' THEN 'C : ' | | product_type
ELSE NULL
END AS abc_product_type
FROM Product;
```

#### 总计

rollup(小计1, 小计2,...) 相当于group(), group(小计1), group(小计1, 小计2)

cube(小计1, 小计2,...) 相当于group(), group(小计1), group(小计2), group(小计1, 小计2), 即所有的可能

GROUPING SETS(小计1, 小计2) 相当于 group(小计1), group(小计2)

```sql
SELECT product_type, regist_date, SUM(sale_price) AS sum_price
FROM Product
GROUP BY ROLLUP(product_type, regist_date);
```

当使用grouping()时 总计, 小计所产生的null值为1, 其他值为0

```sql
SELECT 
CASE WHEN GROUPING(product_type) = 1 THEN ' 商品种类 合计 ' 
ELSE product_type END AS product_type,
CASE WHEN GROUPING(regist_date) = 1 THEN ' 登记日期 合计 '
--数据类型必须相同,所以将日期转换为字符串格式
ELSE CAST(regist_date AS VARCHAR(16)) END AS regist_date,
SUM(sale_price) AS sum_price
FROM Product GROUP BY ROLLUP(product_type, regist_date);
```

## 函数

ABS( 数值 ) 绝对值

MOD( 被除数,除数 ) 取余

dengdengROUND( 对象数值,保留小数的位数 ) 四舍五入

`字符串 1 || 字符串 2 `字符串的拼接 concat Mysql; 字符串1 + 字符串2 SQL Server

LENGTH( 字符串 ) 长度

LOWER( 字符串 ) 小写

UPPER( 字符串) 大写

COALESCE(字符串1, 字符串2...) 取第一个有值的.

REPLACE( 对象字符串,替换前的字符串,替换后的字符串 ) 替换

SUBSTRING (对象字符串 FROM 截取的起始位置 FOR 截取的字符数) 截取

CURRENT_DATE 当前日期 年-月-日

CURRENT_TIME 当前时间 时:分:秒

CURRENT_TIMESTAMP 当前日期+时间

EXTRACT( 日期元素 FROM 日期 ) 获得日期元素 year, month, day, hour, minute, second

CAST (转换前的值 AS 想要转换的数据类型) 数据类型转换

## 视图

不保存数据,而是保存SQL语句, 因此节省存储设备容量, 提高代码重用

#### 创建视图

create view 视图名(视图列名) as select语句

#### 注意

不能使用order by语句

可以建立多层视图,但是不推荐

以下都满足时可以进行更新,更新时会更改表数据

- SELECT 子句中未使用 DISTINCT
- FROM 子句中只有一张表
- 未使用 GROUP BY 子句
- 未使用 HAVING 子句

## 子查询

一次性视图

```sql
SELECT product_type, cnt_product FROM 
(SELECT product_type, COUNT(*) AS cnt_product FROM Product GROUP BY product_type ) AS ProductSum;
```

#### 标量子查询

生成一个值,用于判断

```sql
SELECT product_id, product_name, sale_price FROM Product 
WHERE sale_price > (SELECT AVG(sale_price) FROM Product);
```

#### 关联子查询

```sql
SELECT product_type, product_name, sale_price FROM Product AS P1 WHERE sale_price > 
(SELECT AVG(sale_price) FROM Product AS P2
WHERE P1.product_type = P2.product_type 
GROUP BY product_type);
```

## 集合运算

行的运算

并集, union, 会去重; union all, 不去重

交集, intersect, 回去重; intersect all 不去重

差集, except, 保留的是第一个的不同点

```sql
SELECT product_id, product_name FROM Product
UNION 
SELECT product_id, product_name FROM Product2;
```

#### 注意事项

列数相同, 类型一致, order by 只能在最后运行一次

## 联结

列的运算

#### 内联结

表A inner join 表B on 联结条件 where 筛选条件

```sql
SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name, P.sale_price 
FROM ShopProduct AS SP INNER JOIN Product AS P 
ON SP.product_id = P.product_id;
```

#### 外联结

表A left outer join 表B  on 联结条件 where 筛选条件

left 显示表A所有内容, right 显示表B所有内容

```sql
SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name, P.sale_price 
FROM Product AS P LEFT OUTER JOIN ShopProduct AS SP 
ON SP.product_id = P.product_id;
```

#### 交叉联结

生成很多的行 表A行数* 表B行数

```sql
SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name
FROM ShopProduct AS SP CROSS JOIN Product AS P
```

## 窗口函数

只能用于select子句中, 不会有汇总功能, 依然有很多行

```sql
< 窗口函数 > OVER ([ PARTITION BY < 列清单 >]         按什么分组, 如果省略, 意味着将所有的值分为一组
ORDER BY < 排序用列清单 >)											按什么排序
```

#### rank

 用于记录排序编号

rank: 1114

DENSE_RANK: 1112

ROW_NUMBER: 1234

这样的结果不一定会按照order by的顺序进行排序, 需要在from Product后重新声明order by

```sql
SELECT product_name, product_type, sale_price,
RANK () OVER ( PARTITION BY product_type ORDER BY sale_price ) 
AS ranking
FROM Product;
```

#### 框架

选定3行计算平均值

之前的使用preceding, 之后的使用following, 同时使用之前之后用

`ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING`

```sql
SELECT product_id, product_name, sale_price,
AVG (sale_price) OVER (ORDER BY product_id
ROWS 2 PRECEDING) AS moving_avg
FROM Product;
```

## 注意事项

1.引号

字符串和日期常数需要使用单引号(')括起来。

设定中文别名时需要使用双引号""

数字常数无需加注单引号(直接书写数字即可)。

2.换行

单词之间需要使用半角空格或者换行符进行分隔。

3.命名

名称必须以半角英文字母作为开头,含有数字,字母,下划线。

4.注释

1 行注释 写在“--”之后,只能写在同一行

多行注释 写在`/*`和`*/`之间,可以跨多行。

5.运算

所有和null有关的计算结果都是null

不等于使用<>

字符串比较时从第一位开始比较

6.真值表

和and 为逻辑积 0 * 1 = 0

或or 为逻辑和 1 + 1 = 1 

not 为反转逻辑

## 练习题

2.1 select product_name, regist_date from Product where regist_date > '2009-04-28';

2.2 什么都没有  因为null使用 is 和 is not

2.3 select product_name, sale_price, purchase_price from Product where sale_price - purchase_price >= 500;

2.4 select product_name, product_type, sale_price * 0.9 - purchase_price as profit from Product where sale_price * 0.9 - purchase_price > 100;

3.1

product_id不存在与分组

SUM(product_name)对字符串求和

GROUP BY product_type在where之前

3.2 select product_type, sum(sale_price) as sum, sum(purchase_price) as sum from Product group by product_type   having sum(sale_price) >= sum(purchase_price) *1.5 order by sum(sale_price) desc;

3.3 select * from Product order by regist_date desc, sale_price;

4.1 什么都没有,因为没有提交

4.2 商品编号为主键,不能重复

4.3 insert into ProductMargin select product_id, product_name, sale_price, purchase_price, sale_price - purchase_price as margin from Product where product_id <= '0003';

4.4 

begin transaction;

update ProductMargin set sale_price = 3000 where product_id = '0003';

update ProductMargin set margin = sale_price - purchase_price where product_id = '0003';

commit;

5.1 create view ViewPractice5_1(product_name, sale_price, regist_date) as 

select product_name, sale_price, regist_date from Product where sale_price >= 1000 and regist_date = '2009-09-20';

6.2

select 

sum(case when sale_price <= 1000 then 1 else 0 end) as low_price, 

sum(case when sale_price between 1001 and 3000 then 1 else 0 end) as mid_price, 

sum(case when sale_price > 3000 then 1 else 0 end) as high_price 

from Product;

7.1 所有的

7.2 select COALESCE(P2.shop_id, '不确定'), COALESCE(P2.shop_name, '不确定'), P1.product_id, P1.product_name, P1.sale_price

from Product as P1 left outer join ShopProduct as P2  

on P2.Product_id = P1.Product_id;

8.1 

SELECT product_id, product_name, sale_price, 

MAX (sale_price) OVER (ORDER BY product_id) AS current_max_price 

FROM Product;

8.2 

SELECT COALESCE(cast(regist_date as varchar(11)), '') as regist_date

, SUM(sale_price) AS sum_price

FROM Product 

GROUP BY ROLLUP(regist_date) 

order by regist_date;

