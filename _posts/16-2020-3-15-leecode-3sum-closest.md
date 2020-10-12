---
layout:     post
title: Leecode
subtitle:    3sum-closest
date:       2020-03-15
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


#  题目描述
给出含有n个整数的数组s，找出s中和加起来的和最接近给定的目标值的三个整数。返回这三个整数的和。你可以假设每个输入都只有唯一解。
   例如，给定的整数 S = {-1 2 1 -4}, 目标值 = 1.↵↵   最接近目标值的和为 2. (-1 + 2 + 1 = 2).

# java 代码
```java 
 import java.util.ArrayList;
 import java.util.Arrays;
public class Solution {
    public int threeSumClosest(int[] num, int target) {     
        if(num == null||num.length <= 2){return 0;}          
        int delta = 9999;
        int  res = 0;
        int len = num.length;
        Arrays.sort(num);
        int i = 0;        
        while(i < len - 2){
            int left = i + 1 ;
            int right = len - 1;
            int base = num[i];
            while(left < right){
                int sum = base+num[left]+num[right];   
                int deltaNew = sum - target;
                if(deltaNew == 0) return sum;
                if(Math.abs(deltaNew) < Math.abs(delta)){
                     delta = deltaNew;
                     res = sum;                   
                }
                if(deltaNew > 0){
                    right--;
                }else{
                    left++;
                }
            }
            i++;        
        }     
        return res;
    }
    
}
```