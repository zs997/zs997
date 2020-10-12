---
layout:     post
title: Leecode
subtitle:    LeetCode80-remove-duplicates-from-sorted-array-ii
date:       2020-04-18
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
继续思考题目"Remove Duplicates":

如果数组中元素最多允许重复两次呢？
例如：
给出有序数组 A =[1,1,1,2,2,3],
你给出的函数应该返回length =5,  A 变为[1,1,2,2,3].
# java代码
```java
public class Solution {
    public int removeDuplicates(int[] A) {
        if(A == null){
            return 0;
        }
        if(A.length <= 2){return A.length;}
        //loc指向新数组的末尾的下一个元素
        int loc = 2;
        for(int index = 2;index < A.length; index++){
            if((A[loc-2] == A[loc-1])&&(A[loc-1] == A[index])){
                
            }else{
                A[loc++] = A[index];
            }   
        }        
        return loc;        
    }
}
```