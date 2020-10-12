---
layout:     post
title: Leecode
subtitle:    remove-duplicates-from-sorted-array
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
给定一个已排序的数组，使用就地算法将重复的数字移除，使数组中的每个元素只出现一次，返回新数组的长度。

不能为数组分配额外的空间，你必须使用常熟级空间复杂度的就地算法。
例如，
给定输入数组 A=[1,1,2]，
你给出的函数应该返回length=2，A数组现在是[1,2]。
# java 代码
```java 
public class Solution {
    public int removeDuplicates(int[] A) {
        if(A == null ||A.length == 0){return 0;}
        if(A.length == 1) return 1;
        int slow = 1;
        for(int i = 1;i < A.length; i++){
            if(A[i] == A[i-1]){
                
            }else{
                A[slow] = A[i];
                slow++;
            }
        }
        return slow;
    }
}
```