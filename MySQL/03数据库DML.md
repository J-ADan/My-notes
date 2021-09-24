# 数据库



## 数据库的外键（了解）

```sql
CREATE TABLE IF NOT EXISTS `grade`(
`grade_id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '班级序号',
`grade_name` VARCHAR(10) NOT NULL COMMENT '班级名称',
PRIMARY KEY (`grade_id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;

-- 创建外键
-- 1.设置一个字段外键key
-- 2.给这个外键添加约束（执行引用）
-- KEY `FK_gradeid` (`grade_id`),
-- CONSTRAINT `FK_gradeid` FOREIGN KEY (`grade_id`) REFERENCES `grade` (`grade_id`)
CREATE TABLE IF NOT EXISTS `student`( 
    `id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号', 
    `psw` VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码', 
    `name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名', 
    `sex` VARCHAR(3) NOT NULL DEFAULT '男' COMMENT '性别', 
    `brithday` DATETIME DEFAULT NULL COMMENT '出生日期', 
    `address` VARCHAR(100) DEFAULT NULL COMMENT '住址', 
    `email` VARCHAR(20) DEFAULT NULL COMMENT '邮箱', 
    `grade_id` INT(4) NOT NULL COMMENT '学生的年级',
    PRIMARY KEY (`id`),
    KEY `FK_gradeid` (`grade_id`),
    CONSTRAINT `FK_gradeid` FOREIGN KEY (`grade_id`) REFERENCES `grade` (`grade_id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;
```

![image-20210804164212305](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210804164212305.png)

**删除具有外键关系的表，首先要删除引用别人的表，即从表（含有外键的表），其次再删除被引用的表，即主表**



**创建表之后再添加外键**

```sql
-- 创建外键
-- ALTER TABLE `表名` ADD CONSTRAINT `约束名` FOREIGN KEY (`作为外键的列`) REFERENCES `引用的表`(`引用的列`);
ALTER TABLE `student`
ADD CONSTRAINT `FK_grade` FOREIGN KEY (`grade_id`) REFERENCES `grade`(`grade_id`);
```



在数据库中创建外键的操作都是物理外键，数据库级别的外键，不推荐使用。（避免数据库表太多，造成困扰）

**最佳的实现方法：数据库就是单纯的表，我们可以利用代码去实现外键**

## DML语言（全部记住）

DML语言：数据操作语言

### 添加（insert）

```sql
-- 添加操作：
-- INSERT INTO `表名` (`字段1`,`字段2`,`字段3`,`字段4`) VALUES ('值1','值1','值1','值1');
INSERT INTO `student` (`psw`,`name`,`sex`,`grade_id`) VALUES ('802399','姜富超','女','001');

-- 批量添加操作
INSERT INTO `student` (`psw`,`name`,`sex`,`grade_id`) 
VALUES ('802399','jfz','男','001'),
('802399','jsx','女','002')

-- 不书写字段名
INSERT INTO `student` VALUES ('4','802399','dxy','女','2020-1-1','卡点省','802399',003)
```

**ps：一般插入语句，必须要写字段名，不写字段名一定要与表的字段一一对应，自增的字段在有字段名的时候可以不写，但是没有书写字段名的时候必须加上**



### 修改（update）

```sql
-- 修改表的数据
-- UPDATE `表名` SET `字段` = 值 WHERE 条件;
UPDATE `student` SET `psw` = 123456 WHERE id = 1;

-- 修改多个值
-- UPDATE `表名` SET `字段` [SET `字段] = 值 WHERE 条件;
UPDATE `student` SET `psw` = 123456,`sex` = '男' WHERE id = 3;

-- 通过多个条件定位数据
UPDATE `student` SET `psw` = 8023 WHERE sex = '男' AND id = 3;
```

```sql
-- 更新的值不一定是一个数字或者字符，还有可能是一个变量
UPDATE `student` SET `brithday` = CURRENT_TIMESTAMP WHERE id = 1;
```



**WHERE 条件：可以是大于某个值，也可以是小于某个值，也是可以等于某个值，也可以是区间，也可以是sql语句**

| 操作符             | 说明                               |
| ------------------ | ---------------------------------- |
| =                  | 判断是否等于某个特定的条件         |
| <> 或 !=（不等于） | 判断某个字段是否不等于某个值       |
| >                  | 判断某个字段是否大于某个值         |
| <                  | 判断某个字段是否小于某个值         |
| >=                 | 判断某个字段是否大于等于某个值     |
| <=                 | 判断某个字段是否小于等于某个值     |
| BETWEEN a and b    | 判断某个字段是否在某个区间         |
| AND                | 多个条件一块判断，与Java中&&一致   |
| OR                 | 多个条件一块判断，与Java中\|\|一致 |

**警告：更新，删除，修改某个字段，一定要加上条件，不然会覆盖全部字段**

### 删除（delete）



```sql
-- 删除操作（不要使用），会删除数据某张表库所有的数据
DELETE FROM `student`

-- 删除操作 DELETE FROM `表名` WHERE 条件;
DELETE FROM `student` WHERE id = 1;
```



**TRUNCATE 命令**

作用：完全清空一个数据表，表的结构和索引不会变

```sql
-- TRUNCATE TABLE `表名`
TRUNCATE TABLE `student`
```



**delete 与 truncate 的区别**

相同点：都能删除数据，都不会删除表的结构

不同点：

* truncate 重新设置自增列，计数器归零
* truncate 不会影响事务



delete的问题

delete删除数据库表后，重启数据库

* InnoDB：自增列会从1开始，因为他的数据都是存在内存中的，**断电即失**
* MyISAM：继续上一个增量，数据都是存在文件中，不会丢失。
