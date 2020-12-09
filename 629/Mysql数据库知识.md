### 数据库知识

**数据库概念**

* 按照数据结构来组织、存储和管理数据的仓库

  

**字段类型type-整数**

| username | context          |
| -------- | ---------------- |
| 小米     | 哈哈！抢到沙发了 |
| 小韩     | 我又来了         |

| 数据类型 | 数值范围         |
| -------- | ---------------- |
| tinyint     | -128~127 |
| smallint    | -32768~32767         |
| mediumint | -8388608~8388607 |
| int | -2147483648~2147483647 |
| bigint | +-9.22*10的18次方 |

**设置默认值：eg：状态**

**unsigned:只能存储正数（eg:订单金额、用户id,订单id）**

**zerofill:作用于任何数值类型，用0填充剩余字段空间**

| 数据类型   | 含义                  |
| ---------- | --------------------- |
| char       | 最多255个字符         |
| varchar    | 最多65532个字符       |
| tinytext   | 最多255个字符         |
| text       | 最多65535个字符       |
| mediumtext | 最多2的24次方-1个字符 |
| longtext   | 最多2的32次方-1个字符 |

| 数据类型  | 含义                                |
| --------- | ----------------------------------- |
| date      | 日期,格式：YYYY-MM-DD               |
| time      | 时间，格式：HH:MM:SS                |
| datetime  | 日期时间，格式：YYYY-MM-DD HH:MM:SS |
| timestamp | 功能和datetime相同（但范围较小）    |
| year      | 年份，格式：YYYY                    |

**binary**

* 只用于char和varchar值。当字段指定了该属性时，将以区分大小写的方式排序

**comment**

* 添加注释，备注说明

#### 数据库设计

* 第一范式   无重复 的列
  * 数据库表的每一列都是不可分割的基本数据项，同一列中不能有多个值
  * 每一列属性都是不可再分的，确保每一列的原子性
  * 两列的属性相近或相似或一样，尽量合并属性一样的列，确保不产生冗余数据
* 第二范式    属性完全依赖于主键
* 第三范式    属性不能依赖于主属性

**索引**

* 普通索引 index
* 唯一索引  unique
* 主键           primary  key
* 全文索引    fulltext
* 空间索引     spatial

**索引优点**

* 大大加快数据查询速度
* 通过创建唯一索引，保证数据库表每行数据的唯一性

**索引缺点**

* 维护索引需要耗费数据资源
* 占用磁盘空间
* 影响对标的数据进行增删改的速度

**索引应用**

* INDEX索引     性能优化
* UNIQUE索引  避免数据出现重复（用户名可以为空null）
* PRIMARY所以   标识行

**主键**

* 值唯一
* 不允许NULL值
* 可以在创建表时定义，也可以在创建表之后定义

**auto_increment**

* 自动生成整数值
* 新值为上一次插入的值+1
* 只适用于整数列
* 必须有唯一索引
* 必须具备NOT NULL属性

### 第二范式

* 一个表必须有一个主键
* 且没有包含在主键中的列必须完全依赖于主键，而不能只依赖于主键的一部分。

#### 第三范式

* 非主键列必须直接依赖于主键，不能存在传递依赖

<font color=red>text数据类型是不能索引的</font>

**插入insert-插入完整行**

insert into 表名  values(值1，值2，值3，......);

* 插入值的顺序必须和表中所有列顺序一一对应
* 英文括号、英文引号、英文逗号
* SQL语句不区分大小写
* 多条SQL需要分号分割，单条SQL语句无需分号结束

**插入insert-插入行的一部分**

insert into 表名（列1，列2，列3，...) values(值1，值2，值3，...)

* 可以只给某些列提供值，某些列不提供值
* 必须要给不允许NULL值且没有默认值的列提供值，否则插入不成功

#### 插入insert-插入多行

insert into 表名 （列1，列2，列3，...) values(值1，值2，值3，...),(值1，值2，值3，...)

* 可以提高数据库处理的性能

**查询数据**

* select 列名1 from 表名；
* select 列名1 列名2，列名3 ....from 表名；
* select *from 表名；

**过滤数据-where**

搜索条件，where子句，放在from表名后面

* where子句操作符

  | 操作符  | 说明               |
  | ------- | ------------------ |
  | =       | 等于               |
  | <>      | 不等于             |
  | ！=     | 不等于             |
  | <       | 小于               |
  | <=      | 小于等于           |
  | >       | 大于               |
  | >=      | 大于等于           |
  | between | 在指定的两个值之间 |

  ```my
  SELECT * FROM `user` WHERE uid BETWEEN 2 and 4
  ```

  **空值检查**

  * is null
  * 一个列不包含值，称其包含空值NULL
  * NULL与字段包含0，空字符串或仅仅包含空格不同
  * select * from 'user' where level is Null

**组合where子句**

| 操作符 | 说明             |
| ------ | ---------------- |
| AND    | 与               |
| OR     | 或               |
| IN     | 匹配值，与OR相当 |
| NOT    | 非               |

AND 优先级高于OR,如果提高or的优先级需要加（）；

```mys
select * from 'user' where username='php' or username='admin' and is_admin=1
select * from 'user' where username in ('php','admin')
select * from 'user' where username not in ('php','admin')
```

**like**

| 通配符 | 说明                   |
| ------ | ---------------------- |
| %      | 匹配任意字符，任意次数 |
| _      | 总是匹配一个个字符     |

```mys
SELECT * FROM `user` WHERE username like '%test%'
SELECT * FROM `user` WHERE username like '%test_'
```

**更新数据-update特定行**

update 表名 set 列名1 = 值1，列名2 =值2，...where子句

* 如果不写where子句，将会修改表中所有行

```mys
UPDATE user set username = 'test99' WHERE uid=7
```

**删除数据-delete特定行**

delete from 表名 where子句

* 如果不写where子句，将会删除表中所有行

**排序**

* 默认升序（ASC）排序
* 降序排序DESC
* order by 列名1；
* order by 列名1，列名2；
* order by 列名1 DESC，列名2；
* orderby  列名1DESC,列名2DESC;
* 如果有where子句，放在where子句之后

```mys
select * from 'user' order by level desc
select * from 'user' order by uid asc,level desc
```

**限定结果-limit**两个参数第一个是从第几行开始，第二个参数是第几行结束

* limit 5;
* 第一行为0而不是为1；
* limit1，1；
* 放在where子句、order by 子句之后

```mys
select * from 'user' order by level desc limit 3
 
```

**计算字段**

| 操作符 | 说明 |
| ------ | ---- |
| +      | 加法 |
| -      | 减法 |
| *      | 乘法 |
| /      | 除法 |

```my
SELECT *,price*quantity FROM `orders` 
SELECT *,price*quantity as total FROM `orders` 
```

**使用别名-as**

* 别名是一个字段或值的替换名
* 别名使用as关键字赋予

**汇总数据-聚集函数**

| 函数    | 说明             |
| ------- | ---------------- |
| Avg()   | 返回某列的平均值 |
| Count() | 返回某列的行数   |
| Max()   | 返回某列的最大值 |
| Min()   | 返回某列的最小值 |
| Sum()   | 返回某列值之和   |

```mys
select Avg(price) from 'orders'
select Avg(price) as average from 'orders'
```

**分组汇总-group by----**分组的列

* 指示mysql分组数据，然后对每个组进行聚集
* 必须出现在where子句后，order by子句之前
* 除聚集计算语句外，select语句中的列都必须在group by子句给出

```mys
select count(*) from 'attence'
SELECT date, COUNT(*) FROM `attence` WHERE status=1 GROUP by date
SELECT date, COUNT(*) FROM `attence` WHERE status=1 GROUP by date desc
```

备注：group by 汇总的结果及排序的列，分组后的数据进行过滤--------（having)

**where是用来过滤行级别的数据，**

**分组数据过滤---having**

* where过滤指定的是行而不是分组
* having支持所有where操作符号
* 必须出现在group by之后

```my
select date,count(*) from 'attence' where status=1 group by date having count(*)<3 order by date desc
select date,count(*) as total from attence where status=1 group by date having total<3 order by date desc
```

**select子句顺序**

| 子句     | 说明             | 是否必须使用           |
| -------- | ---------------- | ---------------------- |
| select   | 返回数据         | 是                     |
| from     | 从中检索数据的表 | 从表中选择数据时使用   |
| where    | 行级过滤         | 否                     |
| group by | 分组             | 仅在按组计算聚集时使用 |
| having   | 组级过滤         | 否                     |
| order by | 排序             | 否                     |
| limit    | 限制检索的行     | 否                     |

**连表查询-联结**

```mys
select * from 'news','user' where news.admin_id =user.uid
select news.*,user.username from `news`,`user` where news.admin_id = user.uid
```

**join**推荐使用

* 如果表中有至少一个匹配，则返回行
* 联结条件用特定的on子句而不是where子句
* inner join 和join 是相同的

```mys
select news.*,user.username from `news` join user on news.admin_id = user.uid
```

**left join**---是向左表看齐，没有匹配的用Null 填充

**right join**---是向右表看齐，返回右表的所有行，没有匹配的行用Null 填充

```my
select commit.*,user.username from user rihgt join `comment` on comment.uid=user.uid where uid=7//会出错
select commit.*,user.username from user rihgt join `comment` on comment.uid=user.uid where comment.uid=7
```

**表名也可以起别名**

```my
select c.*,u.username from user as u rihgt join `comment` as c on c.uid=u.uid where c.uid=7
```

**PDO方式的数据访问---连接方式**

* $con = mysql_connect()
* $con = mysqli_connect()
* $con = new mysqli()
* $con = new pdo()

**关闭连接方式**

* mysql_close($con)
* mysqli_close($con)
* con->close()
* $con=null