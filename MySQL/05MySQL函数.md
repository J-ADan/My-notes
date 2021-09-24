# MySQL函数

官网文档：https://dev.mysql.com/doc/refman/5.7/en/



## 常用函数（并不常用）

![image-20210806221304751](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210806221304751.png)

![image-20210806221328814](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210806221328814.png)

![image-20210806221401403](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210806221401403.png)





## 聚合函数（常用）

| 函数名  | 描述   |
| ------- | ------ |
| COUNT() | 计数   |
| SUM()   | 求和   |
| AVG()   | 平均值 |
| MAX()   | 最大值 |
| MIN()   | 最小值 |
| ...     | ...    |



```sql
-- count(`字段`) 会忽略所有的null值
SELECT COUNT(`cardid`) FROM `card_book`

-- count(*) 不会忽略null值
SELECT COUNT(*) FROM `card_book`

-- count(1) 不会忽略所有的null值
SELECT COUNT(1) FROM `card_book`
```

count(*) 与 count(1) 的本质都是计算行数，但是 * 是代表走所有行，1 代表只走一行



```sql
-- 求和
SELECT SUM(`count`) FROM `book`

-- 求平均数
SELECT AVG(`count`) FROM `book`

-- 最大值
SELECT MAX(`count`) FROM `book`

-- 最小值
SELECT MIN(`count`) FROM `book`
```



**group by 分组的条件不能用where书写，要用having**



## 数据库级别的MD5加密

MD5：

**MD5信息摘要算法**（英语：MD5 Message-Digest Algorithm），一种被广泛使用的[密码散列函数](https://baike.baidu.com/item/密码散列函数/14937715)，可以产生出一个128位（16[字节](https://baike.baidu.com/item/字节/1096318)）的散列值（hash value），用于确保信息传输完整一致。MD5由美国密码学家[罗纳德·李维斯特](https://baike.baidu.com/item/罗纳德·李维斯特/700199)（Ronald Linn Rivest）设计，于1992年公开，用以取代[MD4](https://baike.baidu.com/item/MD4/8090275)算法。这套算法的程序在 RFC 1321 标准中被加以规范。1996年后该算法被证实存在弱点，可以被加以破解，对于需要高度安全性的数据，专家一般建议改用其他算法，如[SHA-2](https://baike.baidu.com/item/SHA-2/22718180)。2004年，证实MD5算法无法防止碰撞（collision），因此不适用于安全性认证，如[SSL](https://baike.baidu.com/item/SSL/320778)公开密钥认证或是[数字签名](https://baike.baidu.com/item/数字签名/212550)等用途。

![image-20210807100218169](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210807100218169.png)

