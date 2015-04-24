---
layout: post
title: "Minimum Window Substring"
date: 2015-04-24 20:49:51 +0800
comments: true
categories: LeetCode
---

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

For example,  
S = "ADOBECODEBANC"  
T = "ABC"  
Minimum window is "BANC".

这个问题第一感觉是使用动态规划，但问题后半段要求在O(n)的时间内完成，动态规划肯定是Low了。查看Tag发现写着`Hash Table`,`Two Pointers`。猜测`Hash Table`是用来记录字母的个数，`Two Pointers`一前一后记录着子串的长度。

下面在代码中慢慢说明思路。

``` Java
HashMap<Character,Integer> map = new HashMap<Character,Integer>();
for (int i=0; i< T.length();i++){
    if (map.containsKey(T.charAt(i)))
        map.put(T.charAt(i),map.get(T.charAt(i))+1);
    else
        map.put(T.charAt(i),1);
}
```

首先统计出待搜查字符串中出现的字符和相应的出现次数。然后

``` Java
int left = 0;
int count = 0;
int minLen = S.length() + 1;
int minStart = 0;
for (int right = 0;right<S.length();right++){
    if (map.containsKey(S.charAt(right))){
        map.put(S.charAt(right),map.get(S.charAt(right))-1);
        if (map.get(S.charAt(right)) >= 0)
            count++;
        while(count == T.length())
        {
            if(right-left+1<minLen)
            {
                minLen = right-left+1;
                minStart = left;
            }
            if(map.containsKey(S.charAt(left)))
            {
                map.put(S.charAt(left), map.get(S.charAt(left))+1);
                if(map.get(S.charAt(left))>0)
                {
                    count--;
                }
            }
            left++;
        }
    }
}
```

在for循环中，right变量的作用是向右扩大窗口，找到一个右边界确定的满足要求的子字符串。例如  
S = "AAECDBUAAC"  
T = "ABC"  
我们首先找到的是right=5(从0开始计数)，在这里说明一下，上面代码中的第8行和20行中的判断是为了判别S中像开头`AA`这种字母重复出现的情况。我们可以明显看出right=5时，子串"AAECDB"明显不是最短的子串，于是我们进入while循环开始进行修正。

right右边界已经确定，在while循环中我们是在改变left左边界的值。我们在left和right之间的字符串已经不满足要求时会跳出while循环。上例中就是left=2,扫描过两个A时。上面的代码中对于条件是否满足是用count的值判定，这很巧妙也稍增加了理解难度。

除了上面的说明外，代码中还有一些边界情况的处理，所有代码如下

``` Java
public class Solution {
    public String minWindow(String S,String T){
        if (S == null || S.length() == 0)
            return "";
        HashMap<Character,Integer> map = new HashMap<Character,Integer>();
        for (int i=0;i<T.length();i++){
            if (map.containsKey(T.charAt(i)))
                map.put(T.charAt(i),map.get(T.charAt(i))+1);
            else
                map.put(T.charAt(i),1);
        }
        int left = 0;
        int count = 0;
        int minLen = S.length() + 1;
        int minStart = 0;
        for (int right = 0;right<S.length();right++){
            if (map.containsKey(S.charAt(right))){
                map.put(S.charAt(right),map.get(S.charAt(right))-1);
                if (map.get(S.charAt(right)) >= 0)
                    count++;
                while(count == T.length())
                {
                    if(right-left+1<minLen)
                    {
                        minLen = right-left+1;
                        minStart = left;
                    }
                    if(map.containsKey(S.charAt(left)))
                    {
                        map.put(S.charAt(left), map.get(S.charAt(left))+1);
                        if(map.get(S.charAt(left))>0)
                        {
                            count--;
                        }
                    }
                    left++;
                }
            }
        }
        if(minLen>S.length())
        {
            return "";
        }
        return S.substring(minStart,minStart+minLen);
    }
}
```




