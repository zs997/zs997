---
layout:     post
title: Leecode
subtitle:    swap-nodes-in-pairs
date:       2020-03-09
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---

# 题目描述
将给定的链表中每两个相邻的节点交换一次，返回链表的头指针
例如,
给出1->2->3->4，你应该返回链表2->1->4->3。
你给出的算法只能使用常量级的空间。你不能修改列表中的值，只能修改节点本身。
# 分析
* 写一个函数swap，传入参数是某一节点，作用是将接下来的两个节点交换位置。
* 增设一个头节点domi，首先swap(domi),然后传入domi.next.next。
* 一直进行下去，直到交换完所有节点。
# java代码
```java
public class Solution {
    public ListNode swapPairs(ListNode head) {        
        //if(head == null || head.next == null){return head;}
        ListNode domi = new ListNode(0);
        domi.next = head;
        ListNode pre = domi;
        while(pre != null && pre.next != null && pre.next.next != null){
            swap(pre);
            pre = pre.next.next;
        }    
        return domi.next;
    }
    
    public void swap(ListNode pre){
        ListNode t1 = pre.next;
        ListNode t2 = t1.next;
        t1.next = t2.next;
        t2.next = t1;
        pre.next = t2;
    }
}
```