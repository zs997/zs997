---
layout:     post
title: Leecode
subtitle:    xxx
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
给出一个有序的数组和一个目标值，如果数组中存在该目标值，则返回该目标值的下标。如果数组中不存在该目标值，则返回如果将该目标值插入这个数组应该插入的位置的下标
假设数组中没有重复项。
下面给出几个样例：
[1,3,5,6], 5 → 2
[1,3,5,6], 2 → 1
[1,3,5,6], 7 → 4
[1,3,5,6], 0 → 0

# 分析
* 二分查找，查找过程中，出现目标值返回。
* 循环之后的查找结果，只剩下和target最相近的元素。下标分别是 start 和 end。
* 如果target大于end处的元素，插入点是end + 1。
* 如果target小于start处的元素，插入点是 start（如果目标值正好是start处元素，正好一起考虑，也返回start）。
* 剩下一种情况是target == A[end],则返回end。
# java 代码
```java
public class Solution {
    public int searchInsert(int[] A, int target) {
        if(A == null || A.length == 0 ){return 0;}
        
        int start = 0;
        int end = A.length - 1;
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            if(A[mid] == target){
                return mid;
            }else if(A[mid] < target){
                start = mid;
            }else{
                end = mid;
            }
        }
        
        if(A[end] < target){
            return end+1;
        }else if(A[start] >= target){
            return start;
        }else{
            return end;
        }
        
    }
}
```