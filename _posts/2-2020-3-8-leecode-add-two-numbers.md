---
layout:     post
title: Leecode
subtitle:    add-two-numbers
date:       2020-03-8
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
给定两个代表非负数的链表，数字在链表中是反向存储的（链表头结点处的数字是个位数，第二个结点上的数字是百位数...），求这个两个数的和，结果也用链表表示。
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出： 7 -> 0 -> 8
# 分析
应遵循加法规则，从低位向高位相加，如果有进位要考虑进位。还要考虑链表长度问题。设置指针p1，p2分别指向两个链表，第一个while循环，把他们公共的位相加，每位相加的时候都考虑低位的进位，以及向上的进位，这样可以把两个链表的公共位相加。之后的两个while循环：while(p1 != null)和while(p2 != null)最多只执行一个，这样把长度长的链表也加上了。最后一个if，考虑最后一位是否还有进位。

# java代码
```java
public class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode p1 = l1;
        ListNode p2 = l2;
        
       ListNode head = new ListNode(0);
       ListNode p = head;
        int carry = 0;
        int sum = 0;
         int local = 0;
        while(p1 != null && p2 != null){
             sum = p1.val + p2.val + carry;
             local = sum%10;
            
            p.next = new ListNode(local);
            p = p.next;
            
            carry = sum/10;
           p1 = p1.next;
           p2 = p2.next;
        }
        while(p1 != null){
            sum = p1.val + carry;
            local = sum%10;
            //p1.val = local;
            p.next = new ListNode(local);
            p = p.next;
            
            carry = sum/10;
           p1 = p1.next;
        }
        
         while(p2 != null){
            sum = p2.val + carry;
            local = sum%10;
            //p1.val = local;
            p.next = new ListNode(local);
            p = p.next;
            
            carry = sum/10;
           p2 = p2.next;
        }
        
        if(carry > 0){
             p.next = new ListNode(carry);
        }
        
        return head.next;
        
        
    }
}
```