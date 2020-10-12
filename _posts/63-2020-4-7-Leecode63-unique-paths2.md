---
layout:     post
title: Leecode
subtitle:    Leecode63 unique-paths2
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
继续思考题目"Unique Paths":
一个机器人在m×n大小的地图的左上角（起点，下图中的标记“start"的位置）。
机器人每次向下或向右移动。如果在图中加入了一些障碍，有多少不同的路径？
分别用0和1代表空区域和障碍
例如
下图表示有一个障碍在3*3的图中央。
[↵  [0,0,0],↵  [0,1,0],↵  [0,0,0]↵]
有2条不同的路径机器人要到达地图的右下角。（终点，下图中的标记“Finish"的位置）。
备注：m和n不超过100.
![示意图](https://img-blog.csdnimg.cn/20200408211654469.png)
# 分析
* 类似于Leecode62 unique-paths，不同的是加入了障碍物。
* 首先，初始化可能会遇到障碍物，一旦碰到，之后的位置都是不可达的，因为移动方向的限制。因此之后dp都要设置为0。
*  在递推过程中，如果某点是障碍点，那么该点不可达，dp设置为0。
# java 代码
```java
public class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
      
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        
        int dp [][] = new int [m][n];
        //初始化第0列时，如果碰到了障碍1，说明以下的位置都是不可达的。
        //直接break，那么dp值都为0，表示没有方法可以到达。
        for(int i = 0; i < dp.length; i++){
            if(obstacleGrid[i][0] == 1){
                break;
            }
            dp[i][0] = 1;
            
        }
         //初始化第0行时，如果碰到了障碍1，说明右边的位置都是不可达的。
        //直接break，那么dp值都为0，表示没有方法可以到达。
        for(int j = 0; j < dp[0].length;j++){
             if(obstacleGrid[0][j] == 1){
                break;
            }
            dp[0][j] = 1;
        }
        
        for(int i = 1; i < dp.length;i++){
           for(int j = 1; j <dp[0].length;j++){
               //到新的点时，要判断是不是障碍点，如果是 要设置为0，不可达
               if(obstacleGrid[i][j] == 1){
                   dp[i][j] = 0;
               }else{
                    dp[i][j] = dp[i-1][j] + dp[i][j-1];
               }              
           } 
        }        
        return dp[m-1][n-1];       
    }
}
```