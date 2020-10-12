---
layout:     post
title: Leecode
subtitle:    Leecode61 rotate-list
date:       2020-04-08
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
将给定的链表向右转动k个位置，k是非负数。
例如：
给定1->2->3->4->5->null ， k=2，
返回4->5->1->2->3->null。
# 分析
* 题意是从链表的左侧，循环添加到左侧。k可能很大。
* 发现，如果k和链表长度一致，那么相当于没有转动任何元素，所以有周期的概念，可以用取余概念，等效转动。
* 如果转动的k小于链表长度，相当于从链表的右侧的倒数第n个元素开始，整体拼接到链表的头部。
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
    public ListNode rotateRight(ListNode head, int n){
        if(head == null){
            return head;
        }        
        ListNode fast = head;
        //要知道链表长度
        int len = 0;
        while(fast != null){
            len++;
            fast = fast.next;
        }
        fast = head;
        ListNode slow = head;
        //从右边挪动元素向左，如果和链表长度一样，则n=0。
        //相当于没有动，其他就相当于挪动了小于长度的次数。
        n = n%len;
        //目的是让快指针比慢指针快n个，如果不需要挪动，两指针一样快
        for(int i = 0; i < n; i++){
            fast = fast.next;
        }
       //慢指针最终指向倒数第n+1个元素。
        //即倒数第n个元素的前一个元素。
        //此元素就是新链表的尾部
        while(fast.next != null){
            fast = fast.next;
            slow = slow.next;
        }
        //重新拼接
        //可以看出，当n=0，即挪动很多圈，相当于没动时候，快慢指针同时到表尾，也可以
        fast.next = head;
        head = slow.next;
        slow.next = null;       
        return head;        
    }
}
```