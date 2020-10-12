---
layout:     post
title: Leecode
subtitle:    combination-sum
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
给出一组候选数C和一个目标数T，找出候选数中加起来和等于T的所有组合。
C中的数字在组合中可以被无限次使用
注意：
题目中所有的数字（包括目标数T）都是正整数
你给出的组合中的数字 (a 1, a 2, … , a k) 要按非递增排序 (ie, a 1 ≤ a 2 ≤ … ≤ a k).
结解集中不能包含重复的组合
例如：给定的候选数集是[2,3,6,7]，目标数是7
解集是：
[7]
[2, 2, 3]

# 分析
* 使用回溯法
# java 代码
```java 
import java.util.*;
public class Solution {
    public ArrayList<ArrayList<Integer>> combinationSum(int[] candidates, int target) {
        ArrayList<ArrayList<Integer>> res = new ArrayList<>();
        if(candidates == null || candidates.length == 0 || target <= 0){return res;}
        
        Arrays.sort(candidates);
        combinationSumHelper(candidates,0,target,new ArrayList<Integer>(),res);
        
        return res;
    }
    public void  combinationSumHelper(int [] candidates,int index,int target,ArrayList<Integer> cur,ArrayList<ArrayList<Integer>> res){
         if(target == 0){
             res.add(new ArrayList<Integer> (cur));
         }else if(target > 0){
             for(int i = index; i < candidates.length; i++){
                 if(candidates[i] > target) break;
                 cur.add(candidates[i]);
                 combinationSumHelper(candidates,i,target - candidates[i],cur,res);
                 cur.remove(cur.size()-1);
             }
         }
     }
}
```
