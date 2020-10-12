---
layout:     post
title: Leecode
subtitle:    search-for-a-range
date:       2020-03-17
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
给出一个有序数组，请在数组中找出目标值的起始位置和结束位置
你的算法的时间复杂度应该在O(log n)之内
如果数组中不存在目标，返回[-1, -1].
例如：
给出的数组是[5, 7, 7, 8, 8, 10]，目标值是8,
返回[3, 4].

# 分析
* 二分查找，找起点和终点。使用两次。
* 每次查找完，排除start和end。

# java 代码

```java
public class Solution {
    public int[] searchRange(int[] A, int target) {
        int [] res = {-1,-1};
        if(A == null || A.length == 0){return res;}
        int res1 = -1;
        int res2 = -1;
        int start = 0;
        int end = A.length - 1;
        //寻找左边起点
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            if(A[mid] >= target){
                end = mid;
            }else{
                start = mid;
            }
        }
        //先看左边 start 是不是相等
        if(A[start] == target){
            res1 = start;
        }else if(A[end] == target){
            res1 = end;
        }
        
        
        //寻找右边结束点
         start = 0;
         end = A.length - 1;      
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            if(A[mid] <= target){
                start = mid;    
            }else{
                end = mid;
            }
        }
        //先看右边 是不是相等 扩大范围
        if(A[end] == target){
            res2 = end;
        }else if(A[start] == target){
            res2 = start;
        }
        res[0] = res1;
        res[1] =res2;
        return res;
    }
}
```