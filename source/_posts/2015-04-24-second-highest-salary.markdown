---
layout: post
title: "Second Highest Salary"
date: 2015-04-24 15:00:09 +0800
comments: true
categories: LeetCode
---

Write a SQL query to get the second highest salary from the Employee table.  
If there is no second highest salary,then the query should return `null`

需要查询第二高的薪水，对于有位置要求的查询，我首先想到了`LIMIT`关键字，题目同时要求去重，需要使用`DISTINCT`关键字

``` SQL
SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT 1,1;
```

上面语句的问题是当结果为空时，返回的是`[]`,而不是`null`,解决办法是嵌套SELECT语句

``` SQL
SELECT (SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT 1,1);
```

对于顺序问题的查询，我们也倾向于使用MAX，MIN这些统计函数，当然此问题还可以使用子查询完成，配合使用MAX函数，代码如下

``` SQL
SELECT MAX(Salary)
FROM Employee
WHERE Salary < (SELECT MAX(Salary) FROM Employee);
```
