---
layout:     post
title: Leecode
subtitle:    two-sum
date:       2020-03-8
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
给出一个整数数组，请在数组中找出两个加起来等于目标值的数，
你给出的函数twoSum 需要返回这两个数字的下标（index1，index2），需要满足 index1 小于index2.。注意：下标是从1开始的
假设给出的数组中只存在唯一解
例如：
给出的数组为 {2, 7, 11, 15},目标值为9
输出 ndex1=1, index2=2
# 分析
因为所求是符合值条件的索引，可以使用 HashMap 设计键值对 key:值 value:索引。在数组遍历过程中，将不能产生结果的键值对都存到Map中，如果发现了符合条件的，立即返回结果。
# java 代码
```java
import java.util.Map;
import java.util.HashMap;
public class Solution {
    public int[] twoSum(int[] numbers, int target) {
        Map<Integer,Integer> map = new HashMap<>();
        // number index
        int res [] = new int [2];
        for(int i = 0; i < numbers.length; i++){
            if(map.containsKey(target - numbers[i])){
                res[0] = map.get(target - numbers[i]);
                res[1] = i+1;
                 return res;
            }else{
                map.put(numbers[i],i+1);
            }
        }
        return res;
    }
}
```