---
layout:     post
title: Leecode
subtitle:    first-missing-positive
date:       2020-03-18
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---

# 题目描述
给出一个无序的整数型数组，求不在给定数组里的最小的正整数
例如：
给出的数组为[1,2,0] 返回3,
给出的数组为[3,4,-1,1] 返回2.
你需要给出时间复杂度在O(n)之内并且空间复杂度为常数级的算法
# 分析
* 将数组中所有负数和0，替换成MAX_VALUE
* 一个n维数组，first-miss-positive 一定不大于 n+1
* 遍历一遍数组，遍历过程中：
	* 数组下标为 **i**时 ，**A[i]** 如果不是MAX_VALUE，而且在数组下标范围内出现（如果大于数组的长度n，first-miss-positive也一定不是这个数）。将对应位置的**A[A[i]-1]**，置为负数。表明**A[i]**出现于数组中。	
	*  再次遍历数组的时候，如果某下标**j**出现 A[j] > 0,情况时，说明数字j+1没有出现过。 
# java 代码
```java 
public class Solution {
    public int firstMissingPositive(int[] A) {
        if(A == null || A.length == 0){return 1;}
        
        for(int i = 0; i < A.length; i++){
            if(A[i] <= 0){
                A[i] = Integer.MAX_VALUE;
            }
        }
        
        for(int i = 0; i< A.length; i++){
            int temp = Math.abs(A[i])-1;
            if(temp < A.length){                
                A[temp] = -Math.abs(A[temp]);                           
            }
        }
        for(int i = 0; i < A.length ; i++){
            if(A[i] > 0){
                return i+1;
            }
        }
        return A.length + 1;
        
        
        
        
    }
}
```