---
layout:     post
title: Leecode
subtitle:    LeetCode86-partition-list
date:       2020-04-17
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
给出一个链表和一个值x，以x为参照将链表划分成两部分，使所有小于x的节点都位于大于或等于x的节点之前。
两个部分之内的节点之间要保持的原始相对顺序。
例如：
给出1->4->3->2->5->2和x = 3,
返回1->2->2->4->3->5.
# 分析
* tnl
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
    public ListNode partition(ListNode head, int x) {
        if(head == null){return null;}
        ListNode dummy = new ListNode(0);
        ListNode real = dummy;
        ListNode pre = dummy;
        ListNode cur = head;
        dummy.next = head;
        while(cur != null){
            if(pre == real){
               if(cur.val < x){real = real.next;}
                pre = cur;
                cur= cur.next;               
            }else{
                if(cur.val < x){
                    pre.next = cur.next;
                    cur.next = real.next;
                    real.next = cur;
                    real = real.next;
                    cur = pre.next;
                }else{
                     pre = cur;
                     cur = cur.next;                    
                }
            }
        }
       return dummy.next;        
        
    }
}
```