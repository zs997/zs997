---
layout:     post
title: Leecode
subtitle:  container-with-most-water
date:       2020-03-9
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---

# 题目描述
给定n个非负整数a1，a2，…，an，其中每个数字表示坐标(i, ai)处的一个点。以（i，ai）和（i，0）（i=1,2,3...n）为端点画出n条直线。你可以从中选择两条线与x轴一起构成一个容器，最大的容器能装多少水？
注意：你不能倾斜容器
# 分析
* 设置左右指针，容积是下标只差和两指针中最小的高度乘积。初始时，左右指针分别指向最小和最大的端点。计算初始的容积。
*  因为随着指针的移动，宽度肯定会变小，而影响容积的是最矮的一边，短板效应。所以如果移动高的一方指针，一方面宽度会变小，另一方面短板不会改变，所以容积只会变小。所以，移动短板的指针，可能会使容积变大，直到左右指针重合，这时会找到最大的容积。
# java 代码
```java
public class Solution {
    public int maxArea(int[] height) {
        if(height == null || height.length <2){
            return 0;
        }
        int left = 0;
        int right = height.length - 1;
        int area = 0;        
        while(left < right){
            area = Math.max(area,(right - left)*Math.min(height[left],height[right]));
            if(height[left] < height[right]){
                left ++ ;
            }else{
                right --;
            }
        }        
        return area;
    }
}
```