# mysql

## 1.数据库?

存储数据的仓库

## 2.我们测试为什么要学习数据库?

1.我在界面上做了操作,但是这个操作对不对不清楚,就要去数据库验证是否有内容及内容的正确性

2.我们为了'跑'业务,但界面上数据不足以去完成.我们可以手动修改数据库中的数据,然后刷新就可以'跑'

## 3.数据库的地位

是IT人的基础知识.开发,测试,运维,运营支撑都会数据库

他和Linux一样是基础中的基础

对面试而言,数据库主要在笔试中考,面试中可能会现场出题让你做

从培训角度和工作角度出发,我讲授必须掌握的部分

4.数据库的分类

关系型:mysql.oracle,mssql

非关系型:

​	键值对(内存):redis

​	文档:MongoDB

## 4.安装

略

## 5.navicat

连接名:随意取,一般建议取服务器ip的最后一段(知道是哪台机)

ip:服务器的ip,本机是localhost,其他:输入ip地址

端口:3306(默认但可改)

用户名:root

密码:

## 6.库

1.右键----新建数据库

2.数据库名:随意(全英)

   字符集:utf-8

   排序规则:utf8_general_ci



## 7.表

作为测试的你,不需要去建表

实际工作是:开发建,因为功能是他开发,因此他要根据功能决定数据库表如何处理

为了数据库知识的完备性,还是要讲表和表的各种知识



案例:请完成表的创建

### 1.约束

#### 1.非空 not null

#### 2.唯一 unique

#### 3.主键 primary key

主键=非空+唯一

一般是一个表的第一个字段设定成主键且名一般都叫id或xxid

一个表一般都要有主键(中间表除外)

**mysql中主键设定后一般都勾选上"自动递增",原因是:id会从1,2,3....n,自动的每次加1,这样我就不用管id,因为系统触发+1规则保证id的唯一性**

oracle采用的是:序列+触发器完成mysql的自动递增

#### 4.外键 foreign key

1.一个是2表才有外键的概念

**2.一个表的外键一定是另外一个表的主键**

3.外键的引擎要采用InnoDb,否则无法创建外键



### 2.默认值

如果没值,就给默认值;如果有值,替换默认值



### 3.注释

对给定的字段做注释,方便其他人理解字段含义

工作后,建议开发都把每个字段的注释都写上



### 4.无符号

写入的数据不能带符号(-.!@)

主要是针对整数,小数而言,这个字段只能填正整时勾选"无符号"



### 5.填充零

当位数不够时,在前面补充0





## 8.查询(非常重要)

### 1.简单查询

**完整语法:**

select [distinct] 字段,组函数

from 表

[where 条件]

[group by 字段]

   [having 条件]

[order by 字段]



#### 1. select

```mysql
#1.查询一个字段
select ename from emp;

#2.查询多个字段
select ename,job,sal,empno from emp;

#3.查询所有字段
select * from emp;

#4.运算
select ename+5 from emp;  #没有意义.mysql不报错,其他数据库会报错
#如下可行,要求运算列为数值
select sal*12 from emp;

#如运算列存在空值,运算结果为空
select sal,comm,sal+comm from emp;
#为了解决空的问题,mysql采用ifnull函数,第一个参数:如果有值 第二个参数:如果没值后取的默认值
select sal,comm,sal+ifnull(comm,0) from emp;

#5.别名  as===alias
#我们的客户想一下子就知道字段的意思,而经过各种运算后的字段特别长,不利于一下子就知道含义,因此用别名
select sal,comm,sal+ifnull(comm,0) as 月薪,(sal+ifnull(comm,0))*12 as 年薪 from emp;

#如上,语法是不错的,但不符合工作.别名要求:as不写(推荐);不写中文;见名知意;
#即:推荐全英命名
#哪个字段上有空值,就在原来的纯字段变成ifnull(字段,0)
select sal,comm,sal+ifnull(comm,0) month_sal,(sal+ifnull(comm,0))*12 year_sal from emp;

#6.distinct---去重
select distinct job from emp;
#注意:如下写法,是说把distinct后面的部分看成一个整体,对整体去重,看成:distinct (job,ename)
select distinct job,ename from emp;
select distinct job,deptno from emp;

```

#### 2. from 

```mysql
#别名
#工作后,一个表可能有很多字段,而这些字段有的又很长,记不住啊
#如果用原始的敲法,会很痛苦 :(
#于是我们先
#1.select
#2.from 表 别名
#3.select 后用 别名. ,在弹出的信息中或输入或选择来快速完成要输入的字段
#上班后,一定先别名再select,养成这个习惯对你有好处
select e.xxxx from emp e;

#[补充]
#当多表时,如果select中的字段2个表都有,那要注明具体是哪个表的
#deptno在2个表都有,如要写对,必须声明是哪个表的字段
select deptno from emp,dept; #错误
select dept.deptno from emp,dept; #对,可读性不好
select d.deptno from emp e,dept d; #推荐写法
```



#### 3. where(重要)

```mysql
# 数值
#1.>,<,=,>=<=,<>
select ename,job,sal from emp where sal>2000;

#2.between...and...
select ename,job,sal from emp where sal between 2000 and 3000;


#2.字符串
#1.=
select * from emp where job='MANAGER';

#2.like
#_:匹配1个字符
#%:匹配0个或多个字符
select * from emp where ename like '%A%';

#其他的玩法,全部忘记都可以
A%  __A___  __A___%  %__A___  %__A___%


#3.空值 is null
select * from emp where comm is null;


#4.一串值 in
select * from emp where ename in ('%A%','KING','SMITH','CAI10','凤姐');

#5.取反 not
in					not in
is null 			is not null
like				not like
between...and...	not between...and...

#6.and & or
#and取交集,随着and的增加,数据会越来越少
#工作后,几乎都是and
select * from emp where deptno=30 and job='SALESMAN';

#or取并集,随着or的增加,数据会越来越多
select * from emp where deptno=30 or job='SALESMAN' or ename='SCOTT';

#混合时,and优先级高于or
#如需要编写混合情况时,请用括号包裹and部分,这样方便阅读和维护
select ...
from ...
where ( .... and ... and ...)
or ( ... and ...)	
or ...
or ( ...and ...)
```



练习

```mysql


1.	选择部门30中的雇员

select ename from emp where deptno=30;

2.	列出所有办事员的姓名、编号和部门

select ename,empno,deptno from emp where job='CLERK';

3.	找出佣金高于薪金的雇员

select ename from emp where comm>sal;

4.	找出佣金高于薪金60%的雇员

select ename from emp where comm>sal*0.6;

5.	找出部门10中所有经理和部门20中的所有办事员的详细资料

select * from emp where (deptno=10 and job='MANAGER') or (deptno=20 and job='CLERK');

6.	找出部门10中所有经理、部门20中所有办事员，既不是经理又不是办事员但其薪金>=2000的所有雇员的详细资料

select * from emp where (deptno=10 and job='MANAGER') or (deptno=20 and job='CLERK') or (job not in ('MANAGER','CLERK') and sal>=2000);


7.	找出收取佣金的雇员的不同工作

select distinct job from emp where comm is not null;

8.	找出不收取佣金或收取的佣金低于100的雇员

select ename from emp where comm is null or comm<100;
```



继续

```mysql

1.	查询工资大于2500的员工姓名和工资

select ename,sal from emp where SAL>2500;


2.	查询员工号为7839的员工的姓名和部门号和年薪

select ename,deptno,(sal+ifnull(comm,0))*12 year_sal from emp
where empno=7839;

3.	选择工资不在 5000 到 12000 的员工的姓名和工资

select ename,sal from emp where sal not BETWEEN 5000 and 12000;

4.	选择在 20 或 30 号部门工作的员工姓名和部门号

select ename,deptno from emp where deptno in (20,30);

5.	选择公司中没有管理者的员工姓名及职位

select ename,job from emp where mgr is null;

6.	选择公司中有奖金的员工姓名，工资

select ename,sal from emp where comm is not null;

7.	选择员工姓名的第三个字母是 a 的员工姓名

select ename from emp where ename like '__a%';

8.	选择姓名中有字母 a 或 e 的员工姓名

select ename from emp where ename like '%a%' or ename like '%e%';

9.	显示出表emp表中 ename 以 'e'结尾的员工信息、

select * from emp where ename like '%e';

10.	显示出表 emp 的 上级是 7839,7788, 7782的员工姓名、职位

select ename,job from emp where mgr in (7839,7788, 7782);

```



#### 4. group by

1.组函数(avg,sum,max,min,count)

```mysql
#avg,sum类型必须是数值,max,min,count不限制类型,count不统计null值
select avg(sal) from emp;
select avg(ename) from emp;
select sum(sal) from emp;
select sum(ename) from emp;

select max(hiredate) from emp;
select min(ename) from emp;

select count(*) from emp;
select count(comm) from emp;

#补充:
#1.分组函数做运算是可行的
select sum(sal+ifnull(comm,0)) from emp;

#2.不能使用表达式,得放在where子句中
#犯错几率一般
select avg(sal>1500) from emp;#错误
select avg(sal) from emp where sal>1500;#正确

#3.分组函数不能直接作用在where子句中,得展开写
#很多人容易犯错在这个第三点上
select * from emp where sal>avg(sal);#错误
select * from emp where sal>(select avg(sal) from emp);#正确
select * from emp where sal>(2073.2143);


#2.混合 select 字段,组函数(必会比理解)

#经验:当我写完select,就立刻检查是否有组函数;如果有,想都不用想,马上写 group by,分组规则为:除开组函数外的字段全部参与分组(好好体会)

select job,sum(sal) from emp;#错误 结果无法一一对应
select job,sum(sal) from emp group by ename;#错误   结果无法一一对应
select job,sum(sal) from emp group by job;


select job,sum(sal),ename from emp group by job;#错误  结果无法一一对应
select job,sum(sal),ename from emp group by job,ename;


select sum(sal),ename from emp group by job,ename; #隐藏了啊
select sum(sal) from emp group by job,ename;#隐藏了啊
select ename,job from emp group by job,ename;#隐藏了啊
select job from emp group by job,ename;#隐藏了啊
select count(*) from emp group by job,ename;#隐藏了啊
select min(hiredate),avg(sal) from emp group by job,ename;#隐藏了啊

select job,sum(sal),ename,max(hiredate) from emp group by job,ename;
select job,sum(sal),ename,max(hiredate) from emp group by job;#错误 结果无法一一对应
select job,sum(sal),ename,max(hiredate),count(*),avg(comm) from emp group by job,ename,empno;
select job,sum(sal),max(hiredate),count(*) from emp group by hiredate;#错误

#看表经验:当我打开一个表,如果这个表的数据有相同,我立刻会想到按照这个字段分组有意义(好好体会)
```



#### 5. having(***)

**分组完后**,对数据进行过滤

having必须依附于group by而存在

```mysql
#案例:
select job,sum(sal) from emp group by job having sum(sal)>5500;

#补充:
#1.having中不能使用别名
select job,sum(sal) sum_sal from emp group by job having sum_sal>5500;

#2.只能用select中的字段
select job,sum(sal) sum_sal from emp group by job having sal>5500;

#3.可以随意使用组函数(超级重点,很多人都不理解)
select job,sum(sal) sum_sal from emp group by job having count(*)>=3;

#总结:having中只能使用select中的字段但不能使用别名且不限制组函数(超级重点)
```



**面试忒喜欢问:having和where有什么区别?**

where可单独使用;不能直接写组函数;先过滤后分组

having不能单独使用;随意使用组函数;先分组后过滤



#### 6. order by

```mysql
#排序是针对前面的业务逻辑sql都已经写完,数据都有了,但是显示的顺序不是我想要的,于是排序
#1.升序,默认的 asc,可以不写
select * from emp where deptno in (10,30) or job='CLERK'
order by job asc;

select * from emp where deptno in (10,30) or job='CLERK'
order by job;

#2.降序
select * from emp where deptno in (10,30) or job='CLERK'
order by job desc;

#3.别名
select ename,sal+ifnull(comm,0) month_sal 
from emp
where job='CLERK'
order by month_sal;

#4.位置(不推荐)
select ename,sal+ifnull(comm,0) month_sal 
from emp
where job='CLERK'
order by 2;

#5.多字段排序
#规则:先按照第一个规则,如果有相同才按照第二个规则继续排,以此类推
select * from emp order by deptno desc,sal,comm desc,job,ename,empno;


#思考
select * from emp order by ename;
select * from emp order by ename,mgr desc,job,sal,comm desc;
```





### 2.子查询(必须掌握)

#### 1.子查询解题思路

```mysql
1.	列出至少有1个雇员的所有部门名
2.	列出薪金比"SMITH"多的所有雇员 
3.	列出所有雇员的姓名及其直接上级的姓名 
4.	列出入职日期早于其直接上级的所有雇员
5.	列出部门名称和这些部门的雇员,同时列出那些没有雇员的部门 
6.	列出所有“CLERK”（办事员）的姓名及其部门名称
7.	列出各种工作类别的最低薪金，显示最低薪金大于1500的记录
8.	列出从事“SALES”（销售）工作的雇员的姓名，假定不知道销售部的部门编号
9.	列出薪金高于公司平均水平的所有雇员
10.	列出与“SCOTT”从事相同工作的所有雇员 
11.	列出某些雇员的姓名和薪金，条件是他们的薪金等于部门30中任何一个雇员的薪 
12.	列出某些雇员的姓名和薪金，条件是他们的薪金高于部门30中所有雇员的薪金
13.	列出每个部门的信息以及该部门中雇员的数量
14.	列出所有雇员的雇员名称、部门名称和薪
15.	列出各种类别工作的最低工资
16.	列出各个部门的MANAGER（经理）的最低薪金
17.	列出按年薪排序的所有雇员的年薪
18.	列出按年薪排名的所有雇员的年薪
19.	列出按年薪排序的第四名雇员的年薪
20.	列出薪金水平处于第四位的雇员



1.	查询和 BLAKE相同部门的员工姓名和工资
3.	查询各部门中工资比本部门平均工资高的员工的员工号, 姓名和工资
4.	查询和姓名中包含字母L 的员工在相同部门的员工的员工号和姓名
5.	查询在部门为RESEARCH 的部门工作的员工的员工号
6.	查询上级领导是 KING 的员工姓名和工资
7.	查询平均工资最低的部门信息
8.	查询平均工资最低的部门信息和该部门的平均工资
9.	查询平均工资最高的 job 信息
10.	查询平均工资高于公司平均工资的部门
12.	各个部门中 最高工资中最低的那个部门的 最低工资是多少
13.	查询平均工资最高的部门的MANAGER的详细信息: ename, deptno, job,sal



技巧:
1.知道什么求什么 (select  求......   (链接部分)   where 知道)
2.一列对一列  (where中注意列的个数)
3.死守一条唯一的通道  通道id是和外界打交道的biao select ,,, from ... where 通道id=(select ... from .... 逻辑)
4.在from上做子查询
select ....
from 原始,() a
where a.xxx=原始.xxx
5.先写完整题目,然后再删除掉不看的字段(9题)


```



#### 2.全,内,左(外),右(外)链接(必会)

```mysql
select * from emp,dept;
#数学界:笛卡尔积
#编程界:hash算法
#sql界:全链接  select * from emp full join dept;

select * from emp,dept where emp.deptno=dept.deptno; #内链接

select * from emp inner join dept on emp.deptno=dept.deptno;


select * from emp left join dept on emp.deptno=dept.deptno;#左链接
select * from emp right join dept on emp.deptno=dept.deptno;#右链接


#具体数据展示:
a		b
id		id
1		 1
2		 4
3		 7
4    	 8
5
6

select * from a,b;24
select * from a,b where a.id=b.id;
id 		id
1	  	1
4		4
select * from a left join b on a.id=b.id;
id  	id 
1		1
2
3
4		4
5
6
select * from a right join b on a.id=b.id;
id  	id 
1		1
4		4
		7
		8
		
		
#
class
id	name  		remark
1	20210401	帅哥班
2   20210420	美女班
3	20210515    人才班

student
id	name sex school ..... cid
1	张飞					 1
2	刘备					 1
3	关羽					 1
4	小乔					 2

#第一次写
select c.name,count(s.name)
from class c,student s
where c.id=s.cid
group by c.name;

c.name	    count(s.name)
20210401	3
20210420	1



#第二次写
select c.name,count(s.name)
from class c left join student s
on c.id=s.cid
group by c.name;


c.name	    count(s.name)
20210401	3
20210420	1
20210515	0

#补充:oracle数据库在左右链接上采用(+)的形式(自学),而mysql采用传统的left join等
#left join等是适用于所有数据库
select dname,count(ename)
from dept, emp
where dept.deptno=emp.deptno(+)
group by dname;

```





#### 3. limit(分页)

```mysql
limit x,y
x:从第几个开始,默认从0
y:取几个


select dname,count(ename)
from dept left join emp
on dept.deptno=emp.deptno
group by dname
limit 1,2;
```





## 9.增删改

### 1.增加

```mysql
#增加 insert
#语法:
insert into 表(字段) values (值);


insert into dept(deptno,dname,loc) values (50,'测试部','岗厦');

#[补充]
#1.如果你要插入的是所有值,可以不写字段这个部分,但不推荐
insert into dept values (50,'测试部','岗厦');

#2.如果要插入大量数据(100w)
datafactory
```



### 2.更新

```mysql
#语法:
update 表
set 字段=值[,字段=值,....]
[where 条件]

#案例
update dept
set deptno=60,loc='深圳福田区'
where dname='测试部1';

```



### 3.删除

```mysql
#语法:
delete from 表 [where 条件]

delete from dept where deptno in (50,60);
```



注意:

1.增删改是很危险的.尤其是更新和删除

​	更新:我的同事和我的学生都经历过因为更新被辞退

​	删除:顺丰事件

2.规避:先查后改

​	update:

1. select * from t_emp where dept_id=(select dept_id from t_dept where dept_name='人事部')
   and quit_date is null;

2. update t_emp where dept_id=(select dept_id from t_dept where dept_name='人事部')
   and quit_date is null;

3. update t_emp set sal=sal*1.3 where dept_id=(select dept_id from t_dept where dept_name='人事部')
   and quit_date is null;

   delete:

4. delete from t_emp where dept_id=(select dept_id from t_dept where dept_name='人事部')
   and quit_date is null;

3.上班后,能不动的尽量不动,仅对数据库做查的操作.如实在要动,找人帮你写个sql





## 10.导入导出

很多人喜欢玩命令,但其实实际工作还是几乎都是图形界面操作即可

导出:转储sql文件

导入:运行sql文件















