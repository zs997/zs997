---
layout:     post
title: Leecode
subtitle:     remove-element
date:       2020-03-16
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---

# 题目描述
给定一个数组和一个值，使用就地算法将数组中所有等于这个值的元素删除，并返回新数组的长度。

元素的顺序可以更改。你不用去关心大于当前数组长度的空间里面存储的值。
# 分析
* 前后两个指针，记作index 和end。
* index指向的元素如果需要删除，用end将其覆盖，end--。
* 这时继续检查index处是否需要删除。
* 如果index指向的元素不需要删除index++。
* 一直到index = end - 1 时循环结束。这时，有可能会有两种情况需要考虑。index处是否是要删除的元素。最后按情况返回。
* 
# java 代码
```java
public class Solution {
    public int removeElement(int[] A, int elem) {
        if(A == null ||A.length == 0){
            return 0;
        }
        int index = 0;
        int end = A.length -1;
        while(index < end){
            if(A[index] == elem){
                A[index] = A[end];
                end--;
            }else{
               index ++; 
            }
        }
        if(A[index] == elem){
            return index;            
        }else{
            return index+1;
        }     
    
        
    }
}
```