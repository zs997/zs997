---
layout:     post
title: Leecode
subtitle:    Leecode53 maximum-subarray
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
请计算给出的数组（至少含有一个数字）中具有最大和的子数组（子数组要求在原数组中连续）
例如：给出的数组为[−2,1,−3,4,−1,2,1,−5,4],
子数组[−2,1,−3,4,−1,2,1,−5,4],具有最大的和:6.
拓展：
如果你已经提出了O(n)的解决方法，请尝试使用分治算法来解决这道题。这道题分治的解法更巧妙一些。


# 分析
* 用curMax记录从遍历位置（包括），向左连续的子数组最大值。
* 同时更新目前已知的最大值，max。
# java 代码
```java
import java.lang.Math;
public class Solution {
    public int maxSubArray(int[] A) {
        int curMax = A[0];
        int max = A[0];
        for(int i = 1; i < A.length; i++){
            curMax = Math.max(curMax+A[i],A[i]);
            max = Math.max(max,curMax);
        }
        return max;
    }
}
```