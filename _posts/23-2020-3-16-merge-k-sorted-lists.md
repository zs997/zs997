---
layout:     post
title: Leecode
subtitle:    merge-k-sorted-lists
date:       2020-03-16
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


#  题目描述
合并k个已排序的链表并将其作为一个已排序的链表返回。分析并描述其复杂度。 
# 分析
* 使用优先级队列，每次出队最小的元素。
* 每次出队之后，将下一个非空节点入队。
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
import java.util.*; 
public class Solution {
    public ListNode mergeKLists(ArrayList<ListNode> lists) {
        if (lists == null || lists.size() == 0)
            return null; 
        PriorityQueue<ListNode> queue = new PriorityQueue<ListNode>(lists.size(), new Comparator<ListNode>() {
            @Override
            public int compare(ListNode o1, ListNode o2) {
                if (o1.val < o2.val)
                    return -1;
                else if (o1.val == o2.val)
                    return 0;
                else
                    return 1;
            }
        }); 
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        
        for(ListNode list:lists){
            if(list != null){
                queue.add(list);
            }
        }
        
        while(!queue.isEmpty()){
            ListNode temp = queue.poll();
            tail.next = temp;
            tail = temp;
            if(temp.next != null){
                queue.add(temp.next);
            }
        }
        
        return dummy.next;
     
    }
}
```