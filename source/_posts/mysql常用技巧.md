---
title: mysql常用技巧
date: 2018-10-19 10:14:15
tags:
---
因为工作需要，自学了一点mysql，因为不是程序员，有些用不到也就没有记
<!-- more -->
## mysql安装和使用
1. mysql安装和启动
   - 下载安装mysql
   - 系统偏好设置中启动mysql server
   - 终端中配置环境
       >第一步：打开终端,输入： cd ~
       会进入~文件夹  
       第二步：然后输入：touch .bash_profile
       回车执行后   
       第三步：再输入：open -e .bash_profile 会在TextEdit中打开这个文件  
       第四步：在结束符前输入export PATH=${PATH}:/usr/local/mysql/bin  
       第五步：然后，保存，退出TextEdit（一定是退出），关闭终端并退出。
   - 登录命令：mysql -u root -p
   - 启动MySQL服务
      >sudo /usr/local/MySQL/support-files/mysql.server start
   - 重启MySQL服务
      >sudo /usr/local/mysql/support-files/mysql.server restart

2. homebrew安装mysql

3. mysql修改root密码
   - 停止MySQL服务
      >sudo /usr/local/mysql/support-files/mysql.server stop
   - 禁止mysql的验证密码
      >cd /usr/local/mysql/bin  
   sudo su ./mysqld_safe --skip-grant-tables &
   - 打开新终端
      >/usr/local/mysql/bin/mysql -u root -p 直接enter
   - 设置新密码
      >UPDATE mysql.user SET authentication_string=PASSWORD('新密码') where User='root';
   - 刷新
      >FLUSH PRIVILEGES;
   - 重启mysql
      >mysql -u root -p  
   输入新密码
   - 重设置密码
      >show databases;  
   SET PASSWORD = PASSWORD('新密码');
4. mysql命令行
   - 连接数据库
      >mysql -u 用户名 -p -h 主机名 -P 端口
   - 选择数据库
      >user database
   - 创建数据库
      >create database
   - 数据库描述
      >show databeses显示数据库信息  
      show table显示表信息  
      show columns from table显示列信息  
      show status显示服务器状态信息  
      show create database显示创建特定数据库  
      show create table显示创建特定表  
      show grants显示用户权限  
      show errors和show warnings显示服务器错误、警告消息
5. 数据导入  
通过navicat导入数据，需要设置主键才能追加，导入模式包括：追加、更新、删除、复制、追加和更新

6. 复制表  
复制表结构：create table 新表 like 旧表   
复制表结构及数据：create table新表 select * from 旧表 

7. 创建索引  
索引也是一张表，该表保存了主键与索引字段，并指向实体表的记录，建立索引会占用磁盘空间的索引文件，索引大大提高了查询速度，同时却会降低更新表的速度，如对表进行INSERT、UPDATE和DELETE，因为更新表时，MySQL不仅要保存数据，还要保存一下索引文件。
   - 查看某张表的索引
     >show index from 表名；
   - 创建普通索引
     >alter table 表名 add index  索引列名
   - 创建聚合索引
     >alter table 表名 add index  (索引列1,索引列2) 
   - 删除某张表的索引
     >drop index 索引名 on 表名;

8. 视图  
利用视图简化复杂的联结查询
   - 创建视图
     >create view
   - 查看创建的视图
     >show create view viewname
   - 删除视图
     >drop view viewname
   - 更新视图
     >create or replace view
   - 在视图上查询
     >select * from viewname
9. mysql不区分大小写

10. explain  
解释mysql如何使用索引来处理select语句以及连接表，帮助选择更好的索引和写出更优化的查询语句
    >explain select...

## 数据查询
>select子句顺序：select>from>where>group by>having>oder by>limit
1. Select
   - select查询
      >SELECT 列名 FROM 表名 where 条件 OFFSET 偏移量 LIMIT 返回数据量
   - 查询table的所有列
     >select \* (通配符) from...
   - 通过表名限定列名
     >select table.column from...
   - select和where中使用表别名
     >select 表别名.列名 from table_name as name(表别名) where...
   - 列的算术计算
     >select a+b,a*b,a-b,a/b from table...
   - 测试计算和函数，省略from
     >select 3*2，返回6  
     select Trim('abc ')，返回abc  
     select Now()，返回当前日期时间
2. where
   - 单个限定条件，字符需要用单引号
     >select * from table where column = ‘字符’  
   select * from table where column >= 数值
   - 多个限定条件，优先级and>or，搞不清顺序用括号()
     >select * from table where column1 = ‘字符’ and columns2 = ‘字符’ or column3 = ‘字符’
   - 限定内容范围，多个值逗号分隔
     >select * from table where column in (a,b,c)  
   select * from table where column not in (a,b,c)
   - 限定数值区间
    >select * from table where column between 100 and 200
   - 空值
     >select * from table where column is null;为null  
     select * from table where column is not null;不为null  
     select * from table where column !='';不为空值
   - 模糊条件，like可以代替=
     >select * from table where column like ‘%M%’
   
     >% 表示0个、1个、多个字符  
      _ 下划线表示一个字符  
      M% 表示查询以M开头的内容  
      %M% 表示查询包含M的所有内容  
      %M_ 表示查询以M在倒数第二位的所有内容  
3. group by
   - group by列
     >select * from table group by column

     >分组中有多行null，会分为一行null
   - 在显示的列上使用COUNT, SUM, AVG,MAX等聚合函数
     >select count(*) from table group by column
   - 数据去重
     >select count(distinct,column) from table group by column
   - 汇总列
     >SELECT COALESCE(column,'汇总') FROM table GROUP BY column WITH ROLLUP;

     >coalesce 来设置一个汇总  
   WITH ROLLUP对一列进行汇总
   - 列别名
     >select column as 列别名 from table where...

     >group by子句中不能使用这个列别名

4. having
   - group by汇总后进行限制
     >SELECT column1, SUM(column2)  FROM table GROUP BY column1 HAVING SUM(column2)>100
   - 替代where过滤
     >select *  from table having count(column) >100

5. order by
   - ASC升序，DESC降序
     >select column as new\_name from table group by column order by new\_name desc
   - 多条件排序
     >select * from table group by column order by column1 desc,column2 asc

6. limit
   - limit x，返回前x行
     >select * from table GROUP BY column ORDER BY column  limit 100

   - limit x,y，表示从x行开始的y行数据
     >select * from table where column > 100 limit 10,100;

7. join  
联合多表查询，Join默认是Inner Join即内联接
   >select * from table1 join table2 on table1.column2 = table2.column2
8. union  
连接两个以上的SELECT语句的结果组合到一个结果集合中
   >SELECT * FROM tables WHERE conditions  
   UNION [ALL | DISTINCT]  
   SELECT * FROM tables WHERE conditions

   >DISTINCT: 默认，去掉重复数据
   ALL: 包含重复数据

9. DISTINCT  
去掉列重复数据，放到所有列名前
   >SELECT DISTINCT 列名1,列名2 FROM 表名

10. 嵌套子查询
    - where嵌套，一般与in、=、!=配合使用
     >select * from tableA where column1 in (select * from tableB where column2 =xxx)

     >select * from tableA where column1 = (select * from tableB where column2 =xxx)
    
     >select * from tableA where column1 > all(select * from tableB where column2 =xxx)
    
    - select嵌套
     >SELECT (SELECT * FROM table1 WHERE conditions ) AS column FROM table2

## 函数
SELECT function(列) FROM 表

1. Aggregate聚合函数
   >AVG() 返回平均值    
   COUNT()  返回行数  
   FIRST() 返回第一个记录的值  
   LAST() 返回最后一个记录的值  
   MAX() 返回最大值  
   MIN()  返回最小值  
   SUM()  返回总和  
   std()  返回标准差  
   var()  返回方差

2. Scalar函数
    >UCASE() 将某个字段转换为大写  
    LCASE() 将某个字段转换为小写  
    Substr(字符串，从哪里开始截，截取长度)提取子字符串 
    LEN()  返回某个文本字段的长度  
    ROUND(数字，位数) 小数四舍五入  
    NOW() 返回当前的系统日期和时间  
    FORMAT() 格式化某个字段的显示方式  

3. concat()  
字符串拼接
   - concat(a,b)
     >select concat(A,B) as name from table...

   - CONCAT_WS(separator,str1,str2)
     >select concat(-,A,B) as name from table...返回A-B

4. str_to_date()  
把字符串转换为日期
   >select str_to_date('2008-4-2 15:3:28','%Y-%m-%d %H:%i:%s');

   >select str_to_date('2008-08-09 08:9:30', '%Y-%m-%d %h:%i:%s');

5. 时间日期函数  
日期时间必须用单引号
    >date()返回日期  
    dayofweek()返回星期几，默认周日第1天  
    Time()返回时间  
    year()返回年  
    month()返回月份  
    week(date,mode)返回周数，mode=0，表示周日是第1天，mode=1，表示周一是第1天

6. Date_Format(date,format)  
format是'%Y-%m-%d %H:%i:%s'表示为'年-月-日 时:分:秒'


7. sum(if())
    >select sum(if(条件, 累加值, 不满足条件时加值))...

## SQLZoo题目练习
1. 有多少年沒有颁发诺贝尔医学奖
   >select count(distinct yr) from nobel where yr not in (SELECT distinct yr FROM nobel where subject='Medicine')
2. 顯示所有國家名字,其首都是國家名字加上”City”
   >SELECT name  FROM world WHERE capital = concat (name,' City')
3. 找出所有首都和其國家名字,而首都要有國家名字
   >SELECT capital,name  FROM world where capital like concat('%',name,'%')
4. 找出所有首都和其國家名字,而首都是國家名字的延伸。你應顯示 Mexico City,因它比其國家名字 Mexico 長。你不應顯示 Luxembourg,因它的首都和國家名相是相同的
   >SELECT name, capital  FROM world WHERE capital like concat (name,'%') and capital != name
5. "Monaco-Ville"是合併國家名字 "Monaco" 和延伸詞"-Ville".顯示國家名字，及其延伸詞，如首都是國家名字的延伸
   >SELECT name, replace(capital,name,'')  FROM world WHERE capital like concat (name,'%') and capital != name
6. 顯示歐洲的國家名稱name和每個國家的人口population。以德國的人口的百分比作人口顯示
   >select name,concat(round((population/(select population from world where name='Germany'))*100,0),'%') from world where continent ='Europe' 
7. 哪幾年頒發了物理獎，但沒有頒發化學獎?
   >select distinct yr from nobel where yr in (select yr from nobel where subject='Physics') and yr not in( select yr from nobel where subject='Chemistry')
8. 列出誰獲得多於一個诺贝尔獎項(Subject)
   >select winner from nobel group by winner having count(distinct subject)>1
9. 哪年哪獎項，是同一獎項(subject)頒發給3個人。只列出2000年及之後的資料
   >select yr,subject from nobel where yr>=2000 group by yr,subject having count(subject)=3
10. 列出1962年首影的電影及它的第1主角
    >select movie.title,actor.name from movie,actor,casting where movie.id=casting.movieid and casting.actorid=actor.id and casting.ord=1 and movie.yr='1962'
11. 列出演員茱莉·安德絲'Julie Andrews'曾參與的電影名稱及其第1主角。
    >select movie.title,actor.name  from movie,actor,casting where movie.id=casting.movieid and casting.actorid=actor.id and movieid in(select movieid from casting where actorid in (select actor.id from actor where  name='Julie Andrews')) and ord=1
12. 列出演員茱莉·安德絲'Julie Andrews'曾主演的電影名稱
    >select movie.title  from movie,actor,casting where movie.id=casting.movieid and casting.actorid=actor.id and actor.name='julie andrews' and ord=1
13. 列出1978年首影的電影名稱及角色數目，按此數目由多至少排列
    >select movie.title,count(actorid) from movie,casting where id=movieid and yr=1978  group by title order by count(actorid) desc

补充：  
[mysql下载](https://dev.mysql.com/downloads/)  
[navicat下载](https://navicat.com.cn)  
[SQLZoo在线练习](http://zh.sqlzoo.net)  
[w2school的sql教程](http://www.w3school.com.cn/sql/)