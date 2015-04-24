---
layout: post
title: "Happy Number"
date: 2015-04-24 15:38:59 +0800
comments: true
categories: LeetCode
---

Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

Example: 19 is a happy number

1^2 + 9^2 = 82  
8^2 + 2^2 = 68  
6^2 + 8^2 = 100  
1^2 + 0^2 + 0^2 = 1

我们先分析下算法的终止条件  
成功的情况是计算结果等于1  
失败的情况是陷入了死循环

针对失败的情况，我们可以使用一个Set来记录之前出现过的计算结果，如果出现了重复的计算值，则数字不是Happy Number

在计算的过程中需要求解数字每位的平方值，我们可以从数学角度分解出数字每一位的值，这里为了简单，我直接将数字转化成了字符串，然后遍历字符串的每一位时再将它转化成数字计算。

代码为了简便，使用Python实现，这也可能规避了可能出现的数值溢出的情况

``` Python
class Solution:
    def isHappy(self, n):
        used = set()
        while n != 1 and not n in used:
            used.add(n)
            next = 0
            s = str(n)
            for i in range(len(s)):
                next += int(s[i]) * int(s[i])
            n = next
        if n == 1:
            return True
        return False
```

这个是LeetCode上新的题目，现在还不清楚是否有更加高效的算法，或者这个问题是否有数学解



