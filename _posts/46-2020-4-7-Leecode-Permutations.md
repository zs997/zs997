---
layout:     post
title: Leecode
subtitle:    Leecode46 Permutations
date:       2020-04-07
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---

# 题目描述
给出一组数字，返回该组数字的所有排列
例如：
[1,2,3]的所有排列如下
[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2], [3,2,1].

Given a collection of numbers, return all possible permutations.
For example,
[1,2,3]have the following permutations:
[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2], and[3,2,1].

# 分析
* 排列组合问题，需要用遍历的思想。
* 建立一个List（ArrayList<Integer> curList），用来当做位置，可以抽象成将一些数字不重复地填充到这些位置上。
* 在num数组中挑选没有用过的数字，尝试加入到curList，进入下一个位置操作。
* 一直到所有数字填充完成，则完成一组排列。
* 每一个位置填充一个数字之后，换到下一个位置时，需要删除添加的数字，并且改变使用数字的记录。

# java 代码
```java
import java.util.ArrayList;
public class Solution {
    public ArrayList<ArrayList<Integer>> permute(int[] num) {
        ArrayList<ArrayList<Integer>> res = new ArrayList();
        if(num == null || num.length == 0 ){return res;}        
        boolean visited [] = new boolean[num.length];
        helper(num,visited,new ArrayList<Integer>(),res);        
        return res;
    }
    
    public  void helper(int [] num,boolean [] visited,ArrayList<Integer> curList,ArrayList<ArrayList<Integer>> res){
        if(curList.size() == num.length){
            res.add(new ArrayList<Integer>(curList));            
            return;
        }else{
            for(int i = 0; i < num.length; i++){
                if(!visited[i]){
                    visited[i] = true;
                    curList.add(num[i]);
                    helper(num,visited,curList,res);                    
                    curList.remove(curList.size()-1);
                    visited[i] = false;
                }
            }             
        }
      }
}
```