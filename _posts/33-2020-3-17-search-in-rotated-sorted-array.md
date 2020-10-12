---
layout:     post
title: Leecode
subtitle:    search-in-rotated-sorted-array
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
给出一个转动过的有序数组，你事先不知道该数组转动了多少
(例如,0 1 2 4 5 6 7可能变为4 5 6 7 0 1 2).
在数组中搜索给出的目标值，如果能在数组中找到，返回它的索引，否则返回-1。
假设数组中不存在重复项。

# 分析
.....

# java 代码
```java
public class Solution {
    public int search(int[] A, int target) {
        if(A == null || A.length == 0 ){ return -1;}
        int start = 0;
        int end = A.length - 1;
        
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            if(A[mid] == target){return mid;}
            if(A[mid] > A[start]){
                if(A[start] <= target && A[mid] >= target){
                    end = mid;
                }else{
                    start = mid;
                }
            }else if(A[mid] < A[end]){
                if(A[mid] <= target && A[end] >= target ){
                    start = mid;
                }else{
                    end = mid;
                }    
            }
        }
        if(A[start] == target){return start;}
        if(A[end] == target){return end;}
        return -1;
    }
}
```