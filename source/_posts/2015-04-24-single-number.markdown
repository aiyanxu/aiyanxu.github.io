---
layout: post
title: "LeetCode 之 Single Number"
date: 2015-04-24 13:36:08 +0800
comments: true
categories: LeetCode
---

Given an array of integers,every element appears twice except for one.Find that single one

Note:  
Your algorithm should have a linear runtime complexity.

线性运行时间说明我们最好遍历一次数组就得到结果。在遍历数组的同时，我们需要记住已经出现的数字，这里我们可以使用一个额外的字典。第一版代码如下

``` Java
public class Solution {
    public int singleNumber(int[] A) {
        int res = 0;
        Map<Integer,Integer> tmp = new HashMap<Integer,Integer>();

        for(int i=0; i<A.length; i++){
            if(!tmp.containsKey(A[i]))
                tmp.put(A[i], 1);
            else
                tmp.put(A[i], tmp.get(A[i])+1);
        }

        for(int key : tmp.keySet()){
            if(tmp.get(key) == 1)
                res = key;
        }
        return res;
    }
}
```
上面的代码实现了只遍历一次数组，但之后我们还遍历了一次tmp字典才得到了最终结果，同时我们只需要找出Single Number，是否可以不记录数字出现的具体次数。修改后的第二版代码：

``` Java
public class Solution {
    public int singleNumber(int[] A) {
        HashSet<Integer> tmp = new HashSet<Integer>();
        for(int i=0;i<A.length;i++){
            if(tmp.contains(A[i]))
                tmp.remove(A[i]);
            else
                tmp.add(A[i]);
        }
        return (Integer)(tmp.toArray()[0]);
    }
}
```
在新一版的代码中我们将Hash更换成了Set，因为数组中只有一个Single Number，最后我们只需将Set转换为数组，取出第一个元素即可。

在前面的实现中，我们都使用到了额外的数据结构，如何做到不使用额外空间呢?

在数理逻辑中，我们可以通过异或操作来判定两个数字是否相同。相同的两个数字进行按位异或结果为0，而一个数字与0按位异或结果仍是它之身。根据以上分析，第三版代码如下：

``` Java
public class Solution {
     public int singleNumber(int[] A){
        int res = 0;
        for(int val : A)
            res = res ^ val;
        return res;
    }
}
```
