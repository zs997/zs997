---
layout:     post
title: Leecode
subtitle:    LeetCode116-populating-next-right-pointers-in-each-node
date:       2020-04-18
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---



# 题目描述
格雷码是一种二进制编码系统，如果任意两个相邻的代码只有一位二进制数不同，则称这种编码为格雷码（Gray Code）。
给定一个非负整数n，表示代码的位数，打印格雷码的序列。格雷码序列必须以0开头。
例如：给定n=2，返回[0,1,3,2]. 格雷码的序列为：
00 - 0↵01 - 1↵11 - 3↵10 - 2
注意：
对于一个给定的n，格雷码的序列不一定是唯一的，
例如：根据题目描述，[0,2,3,1]也是一个有效的格雷码序列
# 分析
* 因为同一层的节点具有指向关系，可以使用树的按层遍历。
* 层序遍历可以通过队列实现。
# java 代码
```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */

import java.util.LinkedList;
import java.util.Queue;
public class Solution {
   public void connect(TreeLinkNode root) {
        if(root == null){
            return;
        }
        Queue<TreeLinkNode> queue = new LinkedList<>();
        queue.offer(root);
        TreeLinkNode tail = root;
        while (!queue.isEmpty()){
            //拿出队头
            TreeLinkNode temp = queue.poll();
            //插入左右节点
            if(temp.left != null){
                queue.offer(temp.left);
            }
            //插入左右节点
            if(temp.right != null){
                queue.offer(temp.right);
            }
            //判断是不是该层的最后节点
            if(temp == tail){
                //更新tail为下一层的最后
                tail = ((LinkedList<TreeLinkNode>) queue).peekLast();
            }else{
                temp.next = queue.peek();
            }
        }
    }
}
```