# MySQL索引

1.什么是索引？

一般的应用系统，读写比例在10:1左右，而且插入操作和一般的更新操作很少出现性能问题，在生产环境中，我们遇到最多的，也是最容易出问题的，还是一些复杂的查询操作，因此对查询语句的优化显然是重中之重。说起加速查询，就不得不提到索引了。

2.为什么要有索引呢？

索引在MySQL中也叫做“键”，是存储引擎用于快速找到记录的一种数据结构。索引对于良好的性能
非常关键，尤其是当表中的数据量越来越大时，索引对于性能的影响愈发重要。
索引优化应该是对查询性能优化最有效的手段了。索引能够轻易将查询性能提高好几个数量级。
索引相当于字典的音序表，如果要查某个字，如果不使用音序表，则需要从几百页中逐页去查。



## 索引的分类

索引分类
1.普通索引index :加速查找
2.唯一索引
    主键索引：primary key ：加速查找+约束（不为空且唯一），唯一标识，逐渐不可重复，只能有一个列作为主键
    唯一索引：unique：加速查找+约束 （唯一），避免重复列出现，唯一索引可以重复，多个列都可以标识唯一索引
3.联合索引
    -primary key(id,name):联合主键索引
    -unique(id,name):联合唯一索引
    -index(id,name):联合普通索引
4.全文索引fulltext :用于搜索很长一篇文章的时候，效果最好。
5.空间索引spatial :了解就好，几乎不用



## 索引的使用

1. 在创建表的时候给字段增加索引
2. 创建完毕后增加索引



```sql
-- 显示所有的索引信息 SHOW INDEX FROM `表名`
SHOW INDEX FROM `card_book`
```

```sql
-- 给某个表增加一个索引 ALTER TABLE `表名` ADD FULLTEXT INDEX `索引名`(`列名`)
ALTER TABLE `card` ADD FULLTEXT INDEX `cardname`(`cardname`)
```



## MySQL优化（explain）扩展内容

**explain**

  explain模拟优化器执行SQL语句，在5.6以及以后的版本中，除过select，其**他比如insert，update和delete均可以使用explain查看执行计划**，从而知道mysql是如何处理sql语句，分析查询语句或者表结构的性能瓶颈。
**作用**
1、表的读取顺序
2、数据读取操作的操作类型
3、哪些索引可以使用
4、哪些索引被实际使用
5、表之间的引用
6、每张表有多少行被优化器查询



**explain用法**

explain+SQL语句即可！
执行计划包含的信息如下

| 信息          | 描述                                                         |
| ------------- | ------------------------------------------------------------ |
| id            | 查询的序号，包含一组数字，表示查询中执行select子句或操作表的顺序 **两种情况** id相同，执行顺序从上往下 id不同，id值越大，优先级越高，越先执行 |
| select_type   | 查询类型，主要用于区别普通查询，联合查询，子查询等的复杂查询 1、simple ——简单的select查询，查询中不包含子查询或者UNION 2、primary ——查询中若包含任何复杂的子部分，最外层查询被标记 3、subquery——在select或where列表中包含了子查询 4、derived——在from列表中包含的子查询被标记为derived（衍生），MySQL会递归执行这些子查询，把结果放到临时表中 5、union——如果第二个select出现在UNION之后，则被标记为UNION，如果union包含在from子句的子查询中，外层select被标记为derived 6、union result:UNION 的结果 |
| table         | 输出的行所引用的表                                           |
| type          | 显示联结类型，显示查询使用了何种类型，按照从最佳到最坏类型排序 1、system：表中仅有一行（=系统表）这是const联结类型的一个特例。 2、const：表示通过索引一次就找到，const用于比较primary key或者unique索引。因为只匹配一行数据，所以如果将主键置于where列表中，mysql能将该查询转换为一个常量 3、eq_ref:唯一性索引扫描，对于每个索引键，表中只有一条记录与之匹配。常见于唯一索引或者主键扫描 4、ref:非唯一性索引扫描，返回匹配某个单独值的所有行，本质上也是一种索引访问，它返回所有匹配某个单独值的行，可能会找多个符合条件的行，属于查找和扫描的混合体 5、range:只检索给定范围的行，使用一个索引来选择行。key列显示使用了哪个索引，一般就是where语句中出现了between,in等范围的查询。这种范围扫描索引扫描比全表扫描要好，因为它开始于索引的某一个点，而结束另一个点，不用全表扫描 6、index:index 与all区别为index类型只遍历索引树。通常比all快，因为索引文件比数据文件小很多。 7、all：遍历全表以找到匹配的行 注意:一般保证查询至少达到range级别，最好能达到ref。 |
| possible_keys | 指出MySQL能使用哪个索引在该表中找到行                        |
| key           | 显示MySQL实际决定使用的键(索引)。如果没有选择索引,键是NULL。查询中如果使用覆盖索引，则该索引和查询的select字段重叠。 |
| key_len       | 表示索引中使用的字节数，该列计算查询中使用的索引的长度在不损失精度的情况下，长度越短越好。如果键是NULL,则长度为NULL。该字段显示为索引字段的最大可能长度，并非实际使用长度。 |
| ref           | 显示索引的哪一列被使用了，如果有可能是一个常数，哪些列或常量被用于查询索引列上的值 |
| rows          | 根据表统计信息以及索引选用情况，大致估算出找到所需的记录所需要读取的行数 |
| Extra         | 包含不适合在其他列中显示，但是十分重要的额外信息 1、Using filesort：说明mysql会对数据适用一个外部的索引排序。而不是按照表内的索引顺序进行读取。MySQL中无法利用索引完成排序操作称为“文件排序” 2、Using temporary:使用了临时表保存中间结果，mysql在查询结果排序时使用临时表。常见于排序order by和分组查询group by。 3、Using index:表示相应的select操作用使用覆盖索引，避免访问了表的数据行。如果同时出现using where，表名索引被用来执行索引键值的查找；如果没有同时出现using where，表名索引用来读取数据而非执行查询动作。 4、Using where :表明使用where过滤 5、using join buffer:使用了连接缓存 6、impossible where:where子句的值总是false，不能用来获取任何元组 7、select tables optimized away：在没有group by子句的情况下，基于索引优化Min、max操作或者对于MyISAM存储引擎优化count（*），不必等到执行阶段再进行计算，查询执行计划生成的阶段即完成优化。 8、distinct：优化distinct操作，在找到第一匹配的元组后即停止找同样值的动作。 |



**SQL执行顺序**

想要优化SQL，必须清楚知道SQL的执行顺序，这样再配合explain才能事半功倍！
完整SQL语句

```sql
select distinct 
        <select_list>
from
    <left_table><join_type>
join <right_table> on <join_condition>
where
    <where_condition>
group by
    <group_by_list>
having
    <having_condition>
order by
    <order_by_condition>
limit <limit number>

 1234567891011121314
```

SQL执行顺序

```sql
1、from <left_table><join_type>
2、on <join_condition>
3、<join_type> join <right_table>
4、where <where_condition>
5、group by <group_by_list>
6、having <having_condition>
7、select
8、distinct <select_list>
9、order by <order_by_condition>
10、limit <limit_number>

```

![SQL解析](https://img-blog.csdn.net/20180729102302530?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ppYWRhamluZzI2Nw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)



**extend**

  extended关键字：仅对select语句有效，在explain后使用extended关键字，可以显示filtered列显示了通过条件过滤出的行数的百分比估计值。
  也可以通过show warnings显示扩展信息，输出中的 Message值SHOW WARNINGS显示优化程序如何限定SELECT语句 中的表名和列名， SELECT应用重写和优化规则后的外观，以及可能有关优化过程的其他说明。



## 测试索引

**SQL函数**

![image-20210809203536187](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210809203536187.png)



**索引时间对比**

![image-20210809203926678](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210809203926678.png)



## 索引的原则

* 索引不是越多越好
* 不要对经常变动的数据增加索引
* 小数据量的表的不需要索引
* 索引一般加在常用来查询的字段上

https://blog.csdn.net/wufuhuai/article/details/79631466



