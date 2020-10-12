---
layout:     post
title: Leecode
subtitle:     next-permutation
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
实现函数next permutation（下一个排列）：将排列中的数字重新排列成字典序中的下一个更大的排列。将排列中的数字重新排列成字典序中的下一个更大的排列。
如果不存在这样的排列，则将其排列为字典序最小的排列（升序排列）
需要使用原地算法来解决这个问题，不能申请额外的内存空间
下面有机组样例，左边是输入的数据，右边是输出的答案
1,2,3→1,3,2
3,2,1→1,2,3
1,1,5→1,5,1
# 分析

* 先从末尾向前找出 第一个非升序（这个升序是不严格升序）的下标，如 1 **2** 6642
先找出来标出的2，由于2 后面的数字全是降序，这是后面四位数所能组成的最大数。
* 如果想让整体变大，而且是变大成相邻的数字，可以考虑将 **2**变大一些，因为后面四位数是他们所能组成的最大数了，要想变大，用6642里面比**2**稍微大一些的数替换2，就可以使整体变大一些。
* 剩下的四位数要尽可能小，于是将他们升序排列
* 特殊情况，可能所给的数字是降序的 54321，则直接将其排序。
# java 代码
```java
import java.util.*;
public class Solution {
    public void nextPermutation(int[] num) {
        if(num == null || num.length == 0){return ;}
        
        int last = num.length - 2;
        while(last >=0 && num[last] >= num[last + 1]){
            last--;
        }
        if(last < 0){
            Arrays.sort(num);
            return;
        }
        int i = last + 1;
        while(i < num.length && num[i] > num[last]){
            i++;
        }
        int temp = num[last];
        num[last] = num[i-1];
        num[i-1] = temp;
        //swap(last,i-1);
        //sort(last+1,num.length -1);
        Arrays.sort(num,last + 1,num.length);
    }
}
```