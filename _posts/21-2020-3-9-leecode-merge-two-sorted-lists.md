---
layout:     post
title: Leecode
subtitle:    merge-two-sorted-lists
date:       2020-03-9
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
将两个有序的链表合并为一个新链表，要求新的链表是通过拼接两个链表的节点来生成的。
# 分析
* 新建一个节点，用p指向。l1，l2分别指向要合并的链表。每当遍历进行时，要找出l1和l2之间最小的，用p.next指向它，并且p=p.next。直到两个链表都遍历完，或者其中一个遍历完，退出循环。之后再把没有遍历完的链表连接上。
# java 代码
```java
public class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode head = new ListNode(0);        
        ListNode p = head;        
        while(l1 != null && l2 != null){
            if(l1.val < l2.val){
                p.next = l1;
                l1 = l1.next;
            }else{
                p.next = l2;
                l2 = l2.next;
            }
            p = p.next;
        }        
        if(l1 != null){
            p.next = l1;
        }        
        if(l2 != null){
            p.next = l2;
        }        
        return head.next;
    }
}
```