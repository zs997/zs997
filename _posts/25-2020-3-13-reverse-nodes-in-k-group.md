---
layout:     post
title: Leecode
subtitle:    reverse-nodes-in-k-group
date:       2020-03-13
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
将给出的链表中的节点每k个一组翻转，返回翻转后的链表
如果链表中的节点数不是k的倍数，将最后剩下的节点保持原样
你不能更改节点中的值，只能更改节点本身。
只允许使用常数级的空间
例如：
给定的链表是1->2->3->4->5

对于 k = 2, 你应该返回 2->1->4->3->5

对于 k = 3, y你应该返回 3->2->1->4->5题目描述
将给出的链表中的节点每k个一组翻转，返回翻转后的链表
如果链表中的节点数不是k的倍数，将最后剩下的节点保持原样
你不能更改节点中的值，只能更改节点本身。
只允许使用常数级的空间
例如：
给定的链表是1->2->3->4->5

对于 k = 2, 你应该返回 2->1->4->3->5

对于 k = 3, y你应该返回 3->2->1->4->5

# 分析
* 编写一函数实现节点倒排功能，输入参数为需要改变的链表和需要倒排的范围。
	返回值是倒排部分的尾结点。
* 递归调用此函数，实现全局倒排。
# java代码
```java
public class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        if(k < 2 ){return head;}
        ListNode domi = new ListNode(0);
        domi.next = head;
        ListNode pre = domi;
        while(pre != null){
            pre = reverse(pre,k);
        }
        return domi.next;
    }
    //将pre为头结点 后面的k个节点倒排 返回尾结点
    public ListNode reverse(ListNode pre,int k){        
        ListNode last = pre;
        for(int i = 0; i < k; i++){           
            last = last.next;
             if(last == null){
                return null;
            }
        }
        ListNode tail = pre.next;
        ListNode cur = pre.next.next;
        
        while(cur != null && cur != last){
            tail.next = cur.next;
            cur.next = pre.next;
            pre.next = cur;
            cur = tail.next;
        }
        if(cur == last){
              tail.next = cur.next;
            cur.next = pre.next;
            pre.next = cur;
            cur = tail.next;
        }
        return tail;
       
    }
}
```