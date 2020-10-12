---
layout:     post
title: Leecode
subtitle:    LeetCode81-search-in-rotated-sorted-array-ii
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
继续思考题目 "Search in Rotated Sorted Array":

如果数组种允许有重复元素怎么办？
会影响时间复杂度吗？是怎样影响时间复杂度的，为什么？
编写一个函数判断给定目标值是否在数组中。
# 分析
* 与Leecode33 search-in-rotated-sorted-array类似。不同的是如果A[mid] = A[start],无法判断属于左边或者右边。
# java 代码
```java
public class Solution {
    public boolean search(int[] A, int target) {
         if(A == null || A.length == 0 ){ return false;}
        int start = 0;
        int end = A.length - 1;        
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            if(A[mid] == target){return true;}
            if(A[mid] > A[start]){
                if(A[start] <= target && A[mid] >= target){
                    end = mid;
                }else{
                    start = mid;
                }
            }else if(A[mid] < A[start]){
                if(A[mid] <= target && A[end] >= target ){
                    start = mid;
                }else{
                    end = mid;
                }    
            }else{
                //A[mid] == A[start]  情况不能判断在左边还右边
                //改变左边界 就OK
                start++;
            }
        }
        if(A[start] == target || A[end] == target){
            return true;
        }        
        return false;
    }
}
```