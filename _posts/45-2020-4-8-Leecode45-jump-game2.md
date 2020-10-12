---
layout:     post
title: Leecode
subtitle:    jump-game2
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
给出一个非负整数数组，你最初在数组第一个元素的位置
数组中的元素代表你在这个位置可以跳跃的最大长度
你的目标是用最少的跳跃次数来到达数组的最后一个元素的位置
例如
给出数组 A =[2,3,1,1,4]

最少需要两次才能跳跃到数组最后一个元素的位置。（从数组下标为0的位置跳长度1到达下标1的位置，然后跳长度3到数组最后一个元素的位置）


# java 代码
```java
public class Solution {   
    public int jump(int[] A) {
        if(A == null || A.length <2){
            return 0;
        }
        // dp存放到各点的最小步数，初始化都为0，但只有A[0]处步数为0，其他不可能是0
          int[] dp = new int[A.length]; 
          for(int i = 0; i < A.length; i++){
              //各点所能到达的最远位置
              int maxReach = Math.min(A[i]+i,A.length-1);
              for(int j = i + 1; j <= maxReach; j++){
                  //通过i点 跳跃到j点
                  if(dp[j] == 0){
                      dp[j] = dp[i] + 1;
                  }
              }
             if(dp[A.length - 1] != 0)
                 break;
          }
        return dp[A.length-1];
    }
}
```