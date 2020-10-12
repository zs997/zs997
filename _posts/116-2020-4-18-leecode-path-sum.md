---
layout:     post
title: Leecode
subtitle:    xxx
date:       2020-xx-xx
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
给定一个二叉树和一个值sum，判断是否有从**根节点到叶子节点**的节点值之和等于sum的路径，
例如：
给出如下的二叉树，sum=22，
              5↵             / ↵            4   8↵           /   / ↵          11  13  4↵         /      / ↵        7    2  5   1
返回true，因为存在一条路径5->4->11->2的节点值之和为22
# 分析
* 从根节点到叶子节点的路径。可以使用递归的方式。
* 从根节点出发，向子节点迭代的时候，sum减去root的值。
* 判断该节点是不是叶子节点，如果是，比较sum和节点的值。
* 如果不是叶子节点，向左子树或者右子树递归。 
# java 代码
```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {       
        if(root == null){return false;}
        if(root.left == null && root.right == null && root.val == sum){
            return true;
        }
        return hasPathSum(root.left,sum-root.val) || hasPathSum(root.right,sum-root.val);   
    }  
}
```