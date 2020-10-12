---
layout:     post
title: Leecode
subtitle:    LeetCode83 remove-duplicates-from-sorted-list
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
删除给出链表中的重复元素，使链表中的所有元素都只出现一次
例如：
给出的链表为1->1->2,返回1->2.
给出的链表为1->1->2->3->3,返回1->2->3.
# 分析
* 如 1 1 1 2   3 3，使用cur指针，遍历链表，如果下一个节点元素和本节点元素相同，将下一节点删去，cur不移动。如果下一个节点元素和本节点元素不相同，cur移动。
*  
# java 代码
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
        if(head == null){return head;}
        ListNode cur = head;
        while(cur != null && cur.next != null){
            if(cur.next.val == cur.val){
                cur.next = cur.next.next;               
            }else{
                 cur = cur.next;
            }           
        }
        return head;        
    }
}
```