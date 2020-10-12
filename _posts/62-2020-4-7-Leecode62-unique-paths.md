---
layout:     post
title: Leecode
subtitle:    Leecode62 unique-paths
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
一个机器人在m×n大小的地图的左上角（起点，下图中的标记“start"的位置）。
机器人每次向下或向右移动。机器人要到达地图的右下角。（终点，下图中的标记“Finish"的位置）。
可以有多少种不同的路径从起点走到终点？

![示意图](https://img-blog.csdnimg.cn/20200408211654469.png)
上图是3×7大小的地图，有多少不同的路径？
备注：m和n小于等于100
# 分析
*  建模成二维数组m*n，（0，0）位置表示start，使用动态规划算法求解，dp[i][j] 代表从start点开始到（i,j）点不同的路径数目。
*  因为，机器人每次向下或向右移动。可以从此入手。dp[0][j]，dp[i][0],肯定都是1。
* 任意一点，机器人只能从上方或者是左边过来。故 dp[i][j] = dp[i-1][j] + dp[i][j-1];
# java 代码
```java 
public class Solution {
    public int uniquePaths(int m, int n) {
        int dp [][] = new int [m][n];
        for(int i = 0; i < dp.length; i++){
            dp[i][0] = 1;
        }
        for(int j = 0; j < dp[0].length;j++){
            dp[0][j] = 1;
        }
        for(int i = 1; i < dp.length;i++){
           for(int j = 1; j <dp[0].length;j++){
               dp[i][j] = dp[i-1][j] + dp[i][j-1];
           } 
        }        
        return dp[m-1][n-1];
    }
}
```