# SQL
本文章主要介绍自己在学习数据库的过程中对INNER JOIN和LEFT JOIN 以及RIGHT JOIN的理解

```sql
select s.last_name,s.first_name,d.dept_no
from employees as s left join dept_emp as d
on s.emp_no=d.emp_no;
```

以上是正确的的示范

注意：
INNER JOIN 两边表同时有对应的数据，即任何一边缺失数据就不显示。
LEFT JOIN 会读取左边数据表的全部数据，即便右边表无对应数据。
RIGHT JOIN 会读取右边数据表的全部数据，即便左边表无对应数据。

```sql
select s.last_name,s.first_name,d.dept_no
from  dept_emp as d left join employees as s
on s.emp_no=d.emp_no;
```

这个是无法运行的，因为from后表格顺序必须和前面select读取表格顺序一样

例子：

1：题目描述

查找所有员工的last_name和first_name以及对应部门编号dept_no，也包括展示没有分配具体部门的员工
CREATE TABLE `dept_emp` (
`emp_no` int(11) NOT NULL,
`dept_no` char(4) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`dept_no`));
CREATE TABLE `employees` (
`emp_no` int(11) NOT NULL,
`birth_date` date NOT NULL,
`first_name` varchar(14) NOT NULL,
`last_name` varchar(16) NOT NULL,
`gender` char(1) NOT NULL,
`hire_date` date NOT NULL,
PRIMARY KEY (`emp_no`));

解：

```sql
select s.last_name,s.first_name,d.dept_no
from employees as s left join dept_emp as d
on s.emp_no=d.emp_no;
```

以上的解法用的是外联结法，因为该方法可以查询那些在相关表中没有关联行的行。比如上题中展示没有分配具体部门的员工。

2、题目描述

查找所有已经分配部门的员工的last_name和first_name
CREATE TABLE `dept_emp` (
`emp_no` int(11) NOT NULL,
`dept_no` char(4) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`dept_no`));
CREATE TABLE `employees` (
`emp_no` int(11) NOT NULL,
`birth_date` date NOT NULL,
`first_name` varchar(14) NOT NULL,
`last_name` varchar(16) NOT NULL,
`gender` char(1) NOT NULL,
`hire_date` date NOT NULL,
PRIMARY KEY (`emp_no`));

解：

```sql
select e.last_name ,e.first_name,d.dept_no
from employees as e inner join dept_emp as d
on e.emp_no=d.emp_no;
```

以上解法用的是内部联结，也就是自然连接。自然联结排除多次出现，使每个列只返回一次，而且必须**由我们自己完成这项任务**，选择那些唯一的列。


