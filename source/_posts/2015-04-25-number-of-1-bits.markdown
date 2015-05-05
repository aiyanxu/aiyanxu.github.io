---
layout: post
title: "Number of 1 Bits"
date: 2015-04-25 12:42:38 +0800
comments: true
categories: LeetCode
---

Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the Hamming weight).

For example, the 32-bit integer ’11' has binary representation 00000000000000000000000000001011, so the function should return 3.

问题需要Bit Manipulation，这里选用与操作，初版代码（Python编写）
``` Python
class Solution:
    def hammingWeight(self,n):
        current = 1
        count = 0
        for i in range(32):
            res = current & n
            if res == current:
                count += 1
            current = current << 1
        return count
```
上诉代码存在的问题有：  
1. 将循环次数写定在了代码中，不是一个灵活的方法  
2. current右移，如果n中右边已经出现连续的0位，算法仍然继续，效率低

改进后采用左移思想的代码：
``` Python
class Solution:
    def hammingWeight(self,n):
        count = 0
        while n != 0:
            count += n & 1
            n = n >> 1
        return count
```

从算术角度来看，跟上述的左移思想是类似的
``` Python
class Solution:
    def hammingWeight(self,n):
        count = 0
        while n != 0:
            if n % 2 == 1:
                count += 1
            n /= 2
        return count
```
针对位操作算法我们还可以做出以下优化：
```
class Solution:
    def hammingWeight(self,n):
        count = 0
        while n != 0:
            n &= (n-1)
            count += 1
        return count
```
这其中的思想也可以用来判断一个数字是不是2的整数次幂

