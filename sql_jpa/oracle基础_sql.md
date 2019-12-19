#### 1、Oracle基本示意图

|                           图示                            |            个人理解             |
| :-------------------------------------------------------: | :-----------------------------: |
| ![images\sp190918_084909.png](images\sp190918_084909.png) | ![](images\sp190918_095142.png) |

①数据库:数据磁盘化文件,可以有多个实例,至少一个表空间   

②实例:一系列的后台进程和内存结构组成   

③用户:实例可以创建多个用户   

④模式:一个用户创建对应一个默认模式(缺省为用户名),不同权限   

⑤表空间:用户创建会默认分配一个表空间,一个表空间可以被多个用户使用，可以有多个表文件组成

#### 2、SQL基础

###### (1)语句分类

①DDL数据库定义语句:CREATE、ALERT、DROP   

②DML数据库操作语句:UPDATE、DELETE、INSERT INTO   

③DCL数据库控制语句:GRANT、REVOKE(回收权限)   

④DQL数据库查询语句:SELECT

###### (2)个人知识模糊点

①sql中的null值是不等于null的   

②范围查询:between  and和in()   ③排序:Order by  xxx  DESC/ASC  

④带空值的排序(空值位置):在desc/asc后加nulls first 或nulls last   

⑤oracle中虚拟表:dual

###### (3)函数分类

① 单行函数(作用一行数据):concat(,)  substr(,,)索引从1开始  length()  replace(,,)  round(,)四舍五入  trance(,保留n位)截断小数部分  mod(,)求余  sub(,)  months_between(,)两个时间之间的月份数   nvl(,0)将空值转为0因为任何数与空值计算值位null   nvl2(,,)   initicap、lower、upper、trim、ceil、round、floor

②多行函数(作用一组数据返回一行，又叫组函数、分组函数):AVG、COUNT、MAX、MIN、SUM;一般为select子句或者having子句,select子句时通常和group by合用

#### 3、表间关系

(1)一对多、多对多、一对一

###### (2)多表查询

```sql
--1、内联查询
inner join on
--2、以右表(table2)为主 
right join table2 on 
--3、以左表为主
left join on
--4、全外连接查询,左右两张表数据均全有
full [outer] join table2 on
--5、子查询:跟在from的查询/select/where/多层嵌套等等->结果集:单行单列、单行多列、多行多列、多行单列
--6、where后不能跟聚合函数、having和order by可以
```

#### 4、Oracle基础

###### (1)Oracle常用数据类型

①number(有效位,小数位)   数字类型,整数位为有效位-小数位

②char/nchar、varchar2/varchar/nvarchar      区别:var变长，n为国家字符集

③date/datetime/timestamp   其中最后一个除了时分秒还有时区

###### (2)知识点

①系统时间:sysdate  

②oracle中24小时制:hh24:mm:ss

③Oracle中普通删除会删除到回收站,在删除语句尾部加purge彻底删除

④主键的分类:自然主键、代理主键

⑤表拷贝:create table  表1 as select * from 表2

###### (3)常用函数

```plsql
select distinct 列名，列名 from 表名
/*
  常见函数
*/
-- dual:虚表，为了做临时查询测试使用的
select lower('ABC') from dual;
select upper('abc') from dual;
select initcap('abc') from dual;  --

select concat('a','b') from dual;
select substr('abcdefg',2) from dual;
select length('abc') from dual;
select lpad('abc',15,'*') from dual;  --
select rpad('abc',15,'*') from dual;  --
-- 去掉两边空格，不会去掉中间空格
select trim(' ab cd ') from dual;
select replace('jack and jue','j','bl') from dual;

-- 字符串转日期
select to_date('2019-10-01','yyyy-MM-dd') from dual;
-- 日期转字符串
select to_char(sysdate,'yyyy-MM-dd') from dual;

-- floor,ceil,round
select round(months_between(sysdate,to_date('2016-10-01','yyyy-MM-dd'))) from dual;
```

#### 5、Oracle分页

###### (1)分页

①伪列 rownum/rowid

###### (2)两种分页案例

```sql
--方式1
SELECT * FROM (SELECT ROWNUM AS rowno, t.* FROM emp t WHERE ROWNUM <= 20) table_alias WHERE table_alias.rowno >= 10; 
--方式2
SELECT * FROM (SELECT tt.*, ROWNUM AS rowno FROM (  [SELECT t.* FROM emp t WHERE 条件 ORDER BY xxx, emp_no]) tt WHERE ROWNUM <= 20) table_alias WHERE table_alias.rowno >= 10;
```

#### 6、jdbc

1.驱动加载、获取连接对象

```java
static {
		Properties p = new Properties();
		InputStream in = Thread.currentThread()
            .getContextClassLoader()
            .getResourceAsStream("jdbc.properties");
		try {
            p.load(in);
            Class.forName(p.getProperty("driverClassName"));
			con = DriverManager.getConnection(p.getProperty("url"), 		 
                                              p.getProperty("username"),
                                              p.getProperty("password"));
		} catch (Exception e) {
			throw new RuntimeException("数据库连接失败!");
		}
	}
```

普通语句对象和预编译语句对象区别:前者不预编译，性能低、不能防注入