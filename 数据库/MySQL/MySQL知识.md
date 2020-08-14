# MySQL知识

## 数据库相关SQL

连接数据库：
```
mysql -uroot -p  # u 后面跟用户名 p 后面是密码
```
查看数据库：
```
show databases
```
使用数据库：
```
use databases;
```
查看数据库中的所有表：
```
show tables;
```
创建数据库：
```
create database db_name
```
删除数据库：
```
drop database db_name
```
## 用户相关SQL

### 创建用户
```
create user 'monkey’@'192.168.2.2’ identified by 'passwod’;
# 创建名为 ‘monkey’ 密码为’password’ 登陆IP只能为：192.168.2.2 的用户
 
create user 'monkey’@'192.168.2.%' identified by 'password’;
# 创建名为 ‘monkey’ 密码为’password’ 登陆IP为：192.168.2 网段的用户
 
create user 'monkey’@'%' identified by 'password’;
# 创建名为 ‘monkey’ 密码为’password’ 登陆IP不限的用户
```
### 创建表
```
create table tablename(
                id int auto_increment primary key,
                name varchar(32),
                age int
            )engine=innodb default charset=utf8;
其中 语法：create table +tablename(
                     列名1 类型 其他,
                     列名2 类型 其他) engine = innodb default=charset=utf-8;

engine:指明数据库建表引擎为 innodb （支持事务操作）。
myisam:不支持事务。
default:charset=utf-8 指明数据表的编码字符集 为 utf-8。
```

### 在表中添加数据（三种）
```
insert into tablename(name,age) values('monkey’,18);
             
insert into tablename(name,age) values('JIAJIA’,18),('xiaoliu’,18);
# 可以跟多条记录，一元组的形式添加
             
insert into tablename(name,age) select name,age from tablename2;
# 从别的表查找数据 写入

```

### 删除表中数据不删除表（三种）
```
delete from tablename;    # 删除数据，但是自增计数不会被删除 单纯的清掉数据
truncate table tablename;    # 清空表，相当于新的表 自增计数 0
delete from tb1 where id > 10    # 跟条件
```

### 删除表
```
drop table tablename;    # 删除表
```
### 修改数据
```
update tablename set age=1024;
update tablename set age=2048 where age=18;
```
### 查看数据
```
select * from tablename; # 查看表的所有行列
select  name,age from tablename;    # 查看name和age 列
```
### 条件查询
排序 order by
```
select * form table_name order by id desc    # 从大到小
select * form table_name order by id asc    # 从小到大
```
限制 limit
```
select * form table_name order by id asc limit 10    # 取查询结果的前10条
 
select * form table_name order by id asc limit 20,10    # 取查询结果从第20条开始 往后查10条
 
select * form table_name order by id asc limit 10 offset 20   # 取查询结果从第20条开始 往后查10条
```
模糊查寻 like
```
%表示任意长度的字符  _表示单字符

select * from table_name where name like "张%"    # 以张开头的
 
select * from table_name where name like "%张%"    # 包含张的
 
select * from table_name where name like "%张"    # 以张结尾的
 
select * from table_name where name like "张_"    # 以张开头的 两个字的 
 
select * from table_name where name like "_浩_%"    # 三个字的 并且中间是 浩 的
```
日期查询
```
select * form table_name where date_key between '2019-10-10' and '2019-10-10';
```

### 外键
```
create table tablename1(id int auto_increment primary key ,
name char(32));
 
create table tablename2(id int auto_increment primary key ,
name char(32),
friend_id int,
constraint fk_t1_t2 foreign key (friend_id) references tablename1(id));

　　外键的创建：定义表的列时预料外键字段，之后 constraint fk_t1_t2 foreign key (friend_id) references tablename1(id));   constaint ... foreign key 预留字段名 references 被关联表名（字段名）
```

### 表的补充
```
desc t;    # 查看t 的表结构
         
show create table t;    # 查看创建t的创建语句
         
show create table t \G;    # 横向查看
         
alter table t10 AUTO_INCREMENT=10000;    # 设置自增的起始值
```

## MySQL的自增问题

### 自增的起始值
```
alter table t10 AUTO_INCREMENT=10000;    # 设置自增的起始值
```
### MySQL: 自增步长
#### 基于会话级别：
```
show session variables like 'auto_inc%';    查看全局变量
set session auto_increment_increment=2; 设置会话步长
# set session auto_increment_offset=10;
```
#### 基于全局级别：

```
show global variables like 'auto_inc%'; 查看全局变量
set global auto_increment_increment=2; 设置会话步长
# set global auto_increment_offset=10;
```

### SqlServer：自增步长

#### 基于表级别

```

CREATE TABLE `table1` (
`id` int(11) NOT NULL AUTO_INCREMENT,
) ENGINE=InnoDB AUTO_INCREMENT=3, 步长=2 DEFAULT CHARSET=utf8
# 自增起始值为 3 步长为 2
 
CREATE TABLE `table2` (
`id` int(11) NOT NULL AUTO_INCREMENT,
) ENGINE=InnoDB AUTO_INCREMENT=9, 步长=3 DEFAULT CHARSET=utf8
# 自增起始值为 9 步长为 3
```


```
E_R模型：实体-关系模型

描述两个实体之间的对应规则：
一对一；一对多；多对多；
三范式：
第一范式：1NF 列不可拆分
第二范式：2NF 唯一标识
第三范式:   3NF  引用主键

数据完整性：字段类型，约束

字段类型：
数字 int  decimal(5,2) 一共5位 小数2位
字符串：char ，varchar（可变） text
日期：datetime
布尔：bit

约束
主键：primary key
非空 not null
唯一：unique
默认：default
外键：foreign key

```


## 常用SQL语句

t - table, c - column, v - value, o - operation( = , < , > , <=, >=)

### where中的运算符

| 运算符  | 描述                                         |
| ------- | -------------------------------------------- |
| =       | 等于                                         |
| <>      | 不等于。或（！=）                            |
| >       | 大于                                         |
| <       | 小于                                         |
| \>=的   | 大于等于                                     |
| \<=     | 小于等于                                     |
| between | 在某个范围内                                 |
| like    | 模糊查询,通配符 （%like, %like%, like%,...） |
| in      | 指定针对某个列的多个可能值                   |

### like 通配符

| 通配符                   | 描述                       |
| ------------------------ | -------------------------- |
| %                        | 替代0个或多个字符          |
| _                        | 替代一个字符               |
| [charlist]               | 字符列中的任何单一字符     |
| [^charlist]或[!charlist] | 不在字符列中的任何单一字符 |

```
like 'Tc%' -- 将搜索以字母Tc开头的所有字符串（如 Tccisa）
like '%er' -- 将搜索以字符er结尾的所有字符串（如 teacher）
like '%know%' -- 将搜索在任何位置包含know的所有字符串（如 unknowledgeable）
like '_ove' -- 将搜索以字母ove结尾的所有四个字母的名称（如 love）
like '[CK]ars[eo]n' -- 将搜索下列字符串： Carsen、Karson、Carson和Karson
like '[A-Z]user' -- 将搜索以字符串user结尾、以从A-Z的任何单个字母开头的所有名称
like 'M[^c]%' -- 将搜索以字母M开头，并且第二个字母不是c的所有名称（如MiPro）
```
 


> 关于删除的三个语句： `DROP`, `TRUNCATE`, `DELETE`的区别
>
> **DROP**
>
> ```sql
> drop t;
> ```
>
> 删除表，并释放空间，将test删除的一干二净。
>
> **TRUNCATE**
>
> ```mysql
> truncate t;
> ```
>
> 删除表中的内容，并释放空间，但不删除表的定义，表的结构还在。
>
> **DELETE**
>
> ```mysql
> delete from t;
> ```
>
> 仅删除表test内的所有内容，保留表的定义，不释放空间。

