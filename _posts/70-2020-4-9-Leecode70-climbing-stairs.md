---
layout:     post
title: Leecode
subtitle:    Leecode70 climbing-stairs
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
你在爬楼梯，需要n步才能爬到楼梯顶部
每次你只能向上爬1步或者2步。有多少种方法可以爬到楼梯顶部？
# 分析
* 抽象成斐波那契数列问题。
* 先初始化前两个元素，再用递推关系。

# java 代码
```java
public class Solution {
    public int climbStairs(int n) {
        if(n <= 1){return 1;}
        if(n == 2){return 2;}
        int res = 0;  
         //斐波那契数列问题
        // 1 2 3 5 7 13 ***
        //初始化前两个
        int pre = 1;
        int next = 2;      
        for(int i = 0; i < n-2; i++){
            //拿第一个循环说 res == 3
            res = pre + next;
            //向前移动 pre ==2
            pre = next;
            // next == 3
            next = res;
        }
        return res;      
    }
}
```