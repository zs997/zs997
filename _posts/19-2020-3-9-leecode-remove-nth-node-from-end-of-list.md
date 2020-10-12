---
layout:     post
title: Leecode
subtitle:    remove-nth-node-from-end-of-list
date:       2020-3-9
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---

# 题目描述
给定一个链表，删除链表的倒数第n个节点并返回链表的头指针
例如，
   给出的链表为:1->2->3->4->5, n= 2.↵↵   删除了链表的倒数第n个节点之后,链表变为1->2->3->5.
备注：
题目保证n一定是合法的
请尝试只用一步操作完成该功能
# 分析
* 删除倒数第n个节点可用快慢指针，速度相差n,快指针指到末尾时，慢指针指到要删除的前一个节点
*  同时，要考虑倒数第n个节点可能是头结点。可以设置在头部先插入一个节点，方便操作。
# java代码
```java
public class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
       if(head == null){return head;}
        //if(head.next == null &&n ==1){ return null;}
        ListNode Dump = new ListNode(0);
        Dump.next = head;        
        ListNode p1 = Dump;
        ListNode p2 = Dump;
        for(int i = 0; i < n; i++){
           p1 = p1.next; 
        }
        while(p1.next != null){
            p1 = p1.next;
            p2 = p2.next;
        }
        p2.next = p2.next.next;
        return Dump.next;
    }
}
```