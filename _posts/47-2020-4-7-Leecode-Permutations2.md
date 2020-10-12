---
layout:     post
title: Leecode
subtitle:    Leecode47 Permutation2
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
给出一组可能包含重复项的数字，返回该组数字的所有排列
例如；
[1,1,2]的排列如下：
[1,1,2],[1,2,1], [2,1,1].

# 分析
###### 主体思路和Leecode46 Permutations一致。
* 排列组合问题，需要用遍历的思想。
* 建立一个List（ArrayList<Integer> curList），用来当做位置，可以抽象成将一些数字不重复地填充到这些位置上。
* 在num数组中挑选没有用过的数字，尝试加入到curList，进入下一个位置操作。
* 一直到所有数字填充完成，则完成一组排列。
* 每一个位置填充一个数字之后，换到下一个位置时，需要删除添加的数字，并且改变使用数字的记录。
##### 区别
* 数组中会出现重复数字，导致产生的排列会有重复。
* 为了方便解决问题，先将数组排序。
* 造成重复的地方是:在同一位置，放置数字时，如果放置了大小相同的数字，会产生重复的排列。
* 为了避免这一问题，将数组排序，在某一位置寻找合适数字时，不仅要看该数字是否在之前位置使用过，还要看该位置是否使用过这一数值。


# java 代码
```java
import java.util.ArrayList;
import java.util.Arrays;
public class Solution {
    public ArrayList<ArrayList<Integer>> permuteUnique(int[] num) {
        ArrayList<ArrayList<Integer>> res = new ArrayList();
        if(num == null || num.length == 0 ){return res;}   
        //排序 保证后面算法好使
        Arrays.sort(num);
        boolean visited [] = new boolean[num.length];
        helper(num,visited,new ArrayList<Integer>(),res);        
        return res;
    }
    
    public  void helper(int [] num,boolean [] visited,ArrayList<Integer> curList,ArrayList<ArrayList<Integer>> res){
        if(curList.size() == num.length){
            res.add(new ArrayList<Integer>(curList));            
            return;
        }else{
            //刚开始 肯定没有用过  排好序了 num[0]-1 肯定不会重复出现
            int preNum = num[0]-1;
            //对当前位置挨个选数字
            for(int i = 0; i < num.length; i++){
                //保证之前位置没有用过，且该位置 要尝试的数字不同于上一次的数字 
                if(!visited[i] && preNum != num[i]){
                    //num排好序很关键，让下一个循环 判断是否重复使用过
                    preNum = num[i];
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

