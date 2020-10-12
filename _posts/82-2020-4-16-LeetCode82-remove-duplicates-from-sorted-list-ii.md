---
layout:     post
title: Leecode
subtitle:    LeetCode86-remove-duplicates-from-sorted-list-ii
date:       2020-04-16
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
给出一个排好序的链表，删除链表中的所有重复出现的元素，只保留原链表中只出现一次的元素。
例如：
给出的链表为1->2->3->3->4->4->5, 返回1->2->5.
给出的链表为1->1->1->2->3,  返回2->3.

# 代码实现
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode deleteDuplicates(ListNode head) {
       if(head == null){return null;}
       ListNode dummy = new ListNode(0);
       
       ListNode pre = dummy;
       ListNode cur = head;    
       ListNode real = dummy;
       
       while(cur != null){
           if((pre == dummy ||pre.val != cur.val)&&(cur.next == null ||cur.val != cur.next.val)){
               real.next = cur;
               real = cur;
           }
           pre = cur;
           cur = cur.next;
           pre.next = null;
       }
        
       return dummy.next;
    }
}
```