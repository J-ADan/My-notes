# 数据库DQL语言

DQL（Data Query LANGUAGE）：数据查询语言

* 所有的查询的操作都是用DQL - select
* 不仅仅局限于简单的查询，复杂的查询也可。

**DQL 是数据库中最核心的最重要的语言，使用频率最高的语言**



![image-20210805211913407](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210805211913407.png)

![image-20210806184401592](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210806184401592.png)

**关键字的顺序是不能错的**



## 简单的查询操作

```sql
-- 查询某张表的全部信息 SELECT 字段 FROM `表名`
SELECT * FROM `student`

-- 查询指定的字段 SELECT `字段`,`字段` FROM `表名`
SELECT `name`,`psw` FROM `student`

-- 表头显示自己设置的名字 SELECT `字段` AS 别名,`字段` AS 别名 FROM `表名` AS 别名
SELECT `name` AS 姓名,`psw` AS 密码 FROM `student`

-- 函数 Concat(a,b) 拼接字符串
SELECT CONCAT('名字',`name`) FROM `student`
```

**可以给字段取别名，也可以给表取别名**



## 去重操作

distinct：去重，去除SELECT语句查询出来结果中的重复数据，只显示一条

```sql
-- SELECT DISTINCT `字段` FROM `表名`
SELECT DISTINCT `name` FROM `student`
```



select语句其他语句

```sql
-- 查询系统版本
SELECT VERSION()

-- 查询计算结果
SELECT 100*3-1 AS 计算结果

-- 查询自增的步长
SELECT @@auto_increment_increment

-- 将查询出来的某个字段的数据全部+1
SELECT `grade_id`+1 FROM `student`
```



## where 字句以及逻辑运算符

where字句：检索数据中符合条件的值

搜索的条件可能有一个或者多个，但是返回的结构为布尔值

### 逻辑运算符

| 运算符     | 名称   | 语法               |
| ---------- | ------ | ------------------ |
| and    &&  | 逻辑与 | a and b    a && b  |
| or    \|\| | 逻辑或 | a or b    a \|\| b |
| not    !   | 逻辑非 | not a    !a        |

**建议使用英文**



```sql
-- where 后面跟查询数据需要满足的条件
SELECT `name`,`psw` FROM `student`
WHERE id < 3

-- 查询数据的斗个字段要在某个区间
SELECT `name`,`psw` FROM `student`
WHERE id > 1 AND id < 3

SELECT `name`,`psw` FROM `student`
WHERE id BETWEEN 1 AND 3

SELECT `name`,`psw` FROM `student`
WHERE id > 1 && id < 3

-- 除满足查询条件外的字段
SELECT `name`,`psw` FROM `student`
WHERE NOT id = 2

SELECT `name`,`psw` FROM `student`
WHERE id != 2
```

**注意：BETWEEN ADN 语句是一个闭区间**



## 模糊查询（重点）

**比较运算符：**

| 运算符      | 名称       | 语法                | 描述                          |
| ----------- | ---------- | ------------------- | ----------------------------- |
| IS NULL     | 若为空     | a is null           | 如果操作符为null，则返回真    |
| IS NOT NULL | 若不为空   | a is not null       | 如果操作符不为null，则返回真  |
| BETWEEN AND | 在两个之间 | a between b and c   | 若a在b与c之间，则返回真       |
| LIKE        | 像，包含   | a like b            | SQL匹配，若a匹配b，则返回为真 |
| IN          | 在里面     | a in (a1,a2,a3,...) | a在集合里面，则返回真         |



**like**

```sql
-- 查询名字中姜开头的名字
SELECT `name` FROM `student`
WHERE `name` LIKE '姜%'

-- 查询只有两个字且姜开头的名字
SELECT `name` FROM `student`
WHERE `name` LIKE '姜_'

-- 查询只有三个字，且姜开头的名字
SELECT `name` FROM `student`
WHERE `name` LIKE '姜__'

-- 查询中间有富的名字
SELECT `name` FROM `student`
WHERE `name` LIKE '%富%'

-- % 代表0到多个字符
-- _ 代表一个字符
```



**in**

```sql
-- in 为精确查询语句()内的内容必须与相匹配的内容一致
SELECT `name` FROM `student`
WHERE `name` IN ('jfc','jsx')
```



## 联表查询 JoinON（重难点）

![image-20210806104458077](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210806104458077.png)



```sql
-- 内联查询
SELECT `cardname`,`cardId`
FROM `card` AS c
INNER JOIN `user` AS u
ON u.username = c.cardname

-- 右查询
SELECT `cardname`,`cardId`
FROM `card` AS c
RIGHT JOIN `user` AS u
ON u.username = c.cardname

-- 左查询
SELECT `cardname`,`cardId`
FROM `card` AS c
LEFT JOIN `user` AS u
ON u.username = c.cardname
```

| 操作       | 名称     | 描述                                     |
| ---------- | -------- | ---------------------------------------- |
| inner join | 内联查询 | 如果表中至少有一个匹配，则返回行         |
| right join | 右联查询 | 会从右表中返回所有的值，即使左表没有匹配 |
| left join  | 左联查询 | 会从左表中返回所有的值，即使右表没有匹配 |

**where 与 on**

join on：join + 连接的表 on（判断的条件） + 连接查询

where：等值查询



## 自连接

![image-20210806153327427](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210806153327427.png)



## 分页和排序

**排序：**

* 升序：ASC
* 降序：DESC

```sql
-- 升序：ORDER BY `字段` ASC
SELECT `bookname` FROM `book`
ORDER BY `count` ASC

-- 降序：ORDER BY `字段` DESC
SELECT `bookname` FROM `book`
ORDER BY `count` DESC
```



**分页**

作用：缓解数据库的压力

与之相反的：瀑布流

```sql
-- limit 0,2 从第一个数据开始，显示两个数据
-- limit 1,2 从第二个数据开始，显示两个
-- limit 起始值，页面的大小
-- (n - 1) * pageSize,pageSize
-- (n - 1) * pageSize	起始值
-- pageSize	页面大小
-- n 页面数
-- 数据总数 / 页面大小 = 总页数

SELECT `bookname` FROM `book`
ORDER BY `count` DESC
LIMIT 0,2
```



## 子查询、嵌套查询（由里及外）

where (这个值是计算出来的)

本质：在where语句中写一个查询语句

```sql
-- 子查询、嵌套查询
SELECT c.`cardId`
FROM `card` AS c
WHERE c.`cardname` IN (
SELECT cb.`cardname`
FROM `card_book` AS cb
WHERE cb.`bookname` = 'C语言基础'
)
```



## 分组和过滤

```sql
-- 查询到的数据根据什么来分组
SELECT `bookname` FROM `book`
GROUP BY `count`
HAVING bookname = 'Java编程基础'
```

