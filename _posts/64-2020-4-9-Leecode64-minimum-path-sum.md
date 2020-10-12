---
layout:     post
title: Leecode
subtitle:    Leecode64 minimum-path-sum
date:       2020-04-09
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
给定一个由非负整数填充的m x n的二维数组，现在要从二维数组的左上角走到右下角，请找出路径上的所有数字之和最小的路径。
注意：你每次只能向下或向右移动。
# 分析 
* 题目类似于Leecode62 unique-paths
# java 代码
```java
public class Solution {
    public int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;        
        int dp [][] = new int [m][n];
        //到第(0,0)位置路径长度就是元素(0,0)
        dp[0][0] = grid[0][0];
        //初始化第0列时，路径只能从同一列的上一行过来，因此加本位置的数字。     
        for(int i = 1; i < dp.length; i++){            
            dp[i][0] = dp[i-1][0] + grid[i][0];            
        }
         //初始化第0行时，路径只能从同一行的上一列过来，因此加本位置的数字。     
        for(int j = 1; j < dp[0].length;j++){           
            dp[0][j] = dp[0][j-1] + grid[0][j];
        }        
        for(int i = 1; i < dp.length;i++){
           for(int j = 1; j <dp[0].length;j++){
               //某一点只能从上方或者左边过来。
               dp[i][j] = Math.min(dp[i-1][j],dp[i][j-1])+grid[i][j];        
           } 
        }        
        return dp[m-1][n-1];       
    }
}
```