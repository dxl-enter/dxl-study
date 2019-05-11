## 1 MySQL开发入门
### 1.1 MySQL数据库客户端基础
    （1）www.mysql.com -> downlods -> mysql community -> mysql workbench
### 1.2 MySQL创建表
    ```create table 数据库名.表名(
      `id` int not null auto_increment comment '',
      primary key(`id`) comment ''
    );```
### 1.3 MySQL函数SQL语句
    count(*):查询的数据有几条
    min(birthdate):求最小值
    表名.*: 返回表中的其他数据
    max():求最大值
    sum():求和
### 1.4 MYSQL条件查询
    where 列名 between ‘’ and ‘’ ： 中间
    where 列名 like ‘%王%’：%表示通配符，表示字符串中含有王这个字（模糊查询）数据库效率比较低
### 1.5 MYSQL复杂条件查询
    排序：order by 列名 desc(倒序)/asc(正序，默认)
    多个数据表操作时，必须有关联的字段：
    select * from 表名1，表名2 where 表名1.classid = 表名2.id
    *会消耗数据库性能，网络的性能
    leftjoin：
    select * from 表名1 left join 表名2 on 表名1.classid = 表名2.id
    mysql用join on比较多
