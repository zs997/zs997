---
layout:     post
title: Leecode
subtitle:    LeetCode96-unique-binary-search-trees
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
给定一个值n，能构建出多少不同的值包含1...n的二叉搜索树（BST）？
例如
给定 n = 3, 有五种不同的二叉搜索树（BST）

   1         3     3      2      1↵           /     /      /       ↵     3     2     1      1   3      2↵    /     /                        ↵   2     1         2                 3
# 分析
* 动态规划：dp[i] 表示i个不同的数 比如 1~i 可以形成几个不同的二叉搜索树。
* 若1~i这些数，选出某一个数j作为节点，比它小的数有j-1个，作为左子树。比它大的数有i-j个，作为右子树。这样左子树的数目乘以右子树的数目，就是总共的组合数；从而将所有的可能的节点考虑一遍，完成。
# java 代码
```java
public class Solution {
    public int numTrees(int n) {
        if(n <= 0){return 0;}
        int [] dp = new int [n+1];
        //dp[i] 表示i个不同的数 比如 1~i 可以形成几个不同的二叉搜索树
        dp[0] = 1;
        dp[1] = 1;
        //计算 1~i个节点 可以形成多少二叉树
        for(int i = 2; i <= n; i++){
            //以j号为节点
            for(int j = 1;j<=i;j++){
                //dp[j-1] 左子树形成的树个数  
                //dp[i-j] 右子树 形成的数个数
                dp[i]+= dp[j-1]*dp[i-j];
            }
        }        
        return dp[n];
    }
}
```