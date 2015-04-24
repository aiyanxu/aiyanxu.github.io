---
layout: post
title: "Remove Linked List Elements"
date: 2015-04-24 14:38:12 +0800
comments: true
categories: LeetCode
---

Remove all elements from a linked list of integers that have value val.

Example  
Given: 1-->2-->6-->3-->4-->5-->6,val=6  
return: 1-->2-->3-->4-->5

这道题难度不大，属于在列表中删除特定元素的变种题。需要注意的点一是列表为空的情况，二是头元素需要删除以及删除头元素导致列表为空的情况。直接上代码：

``` Java
public class Solution {
    public ListNode removeElements(ListNode head, int val) {
        if(head == null)
            return null;
        while (head != null && head.val == val){
            head = head.next;
        }
        if(head == null)
            return null;
        ListNode pre = head,p = head;
        while(p != null){
            if(p.val == val){
                pre.next = p.next;
            }
            else{
                pre = p;
            }
            p = p.next;
        }
        return head;
    }
}
```


