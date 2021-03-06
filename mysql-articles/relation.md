# 史上最简单的 MySQL 教程（十八）「关系」

## 关系

在数据库中，将实体与实体的关系反应到表的设计上来，可以细分为 3 种，分别为：一对一`(1:1)`，一对多`(1:N)`（或多对一`(N:1)`）和多对多`(N:N)`。

在此，所有的关系都是指表与表之间的关系。

### 一对一

一对一，即**一张表的一条记录只能与另外一张表的一条记录相对应，反之亦然**。

例如，咱们设计一张「个人信息表」，其字段包含：姓名、性别、年龄、身高、体重、籍贯和居住地等。

![0](http://img.blog.csdn.net/20170601085452637)

如上表所示，基本满足咱们的要求，其中姓名、性别和年龄属于常用数据，但是身高、体重、籍贯和居住地为不常用数据。如果每次查询都要查询所有数据的话，那么不常用数据就会影响效率，而且又不常用。因此，咱们可以将常用的数据和不常用的数据分离存储，即分为两张表，例如：

**表 1：常用数据**

![1](http://img.blog.csdn.net/20170601085511060)

**表 2：不常用数据**

![2](http://img.blog.csdn.net/20170601085527435)

如上面`表1`和`表2`所示，通过字段`ID`，`表1`中的一条记录只能匹配`表2`中的一条记录，反之亦然，这就是`一对一`的关系。

### 一对多/多对一

一对多，即**一张表中的记录可以对应另外一张表中的多条记录，但是反过来，另外一张表中的一条记录只能对应第一张表中的一条记录**。

例如，咱们设计「国家城市表」，其包含两个实体，即国家和城市。

**表 3：国家表**

![3](http://img.blog.csdn.net/20170601085541820)

**表 4：城市表**

![4](http://img.blog.csdn.net/20170601085555233)

如上面`表3`和`表4`所示，通过字段`国家`，`表3`中的一条记录可以匹配`表4`中的多条记录，但反过来，`表4`中的一条记录只能匹配`表3`中的一条记录，这就是典型的`一对多`的关系。

### 多对多

多对多，即**一张表中的记录可以对应另外一张表中的多条记录，反过来，另外一张表中的一条记录也可以对应第一张表中的多条记录**。

例如，咱们设计「教师学生表」，其包含两个实体，即教师和学生。

**表 5：教师表**

![5](http://img.blog.csdn.net/20170601085610524)

**表 6：学生表**

![6](http://img.blog.csdn.net/20170601085624014)

观察上面的`表5`和`表6`，咱们会发现：`表5`和`表6`的设计满足了实体的属性，但没有维护实体之间的关系，即一个老师教过多个学生，一个学生也被多个老师教过。但是无论咱们在`表5`中还是在`表6`中增加字段，都会出现一个问题，那就是：该字段要保存多个数据，并且还是与其他表有关系的字段，不符合设计规范。因此，咱们可以再设计一张「中间表」，专门用来维护`表5`和`表6`的关系。

**表 7：中间表**

![7](http://img.blog.csdn.net/20170601085636952)

观察上面的`表5`、`表6`和`表7`，咱们会发现增加`表7`之后，咱们维护`表5`和`表6`的关系更加方便啦！无论是想从`表5`通过`表7`查到`表6`，还是想从`表6`通过`表7`查到`表5`，都非常容易啦！这就是典型的`多对多`的关系。


----------
———— ☆☆☆ —— [返回 -> 史上最简单的 MySQL 教程 <- 目录](https://github.com/guobinhit/mysql-tutorial/blob/master/README.md) —— ☆☆☆ ————
