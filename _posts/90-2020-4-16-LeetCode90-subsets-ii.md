---
layout:     post
title: Leecode
subtitle:    LeetCode90 subsets-ii
date:       2020-04-16
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
给出一个可能包含重复元素的整数集合S，返回该整数集合的所有子集。
注意：
你给出的子集中的元素要按非递增的顺序排列
给出的解集中不能包含重复的子集
例如：
如果S =[1,2,2], 给出的解集应该是：
[↵  [2],↵  [1],↵  [1,2,2],↵  [2,2],↵  [1,2],↵  []↵]

# 分析
* 与LeetCode78 subsets很类似，但是要考虑重复的情况。
* 法1，在每个位置挑选合适元素，使用回溯算法。
* 法2，每个元素在对应位置，有加入集合和不加入集合的选择，使用回溯算法。但是顺序没有保障，失败。
# 方法1 代码
```java 
import java.util.*; 
public class Solution {
    ArrayList<ArrayList<Integer>> listAll = new ArrayList<>(); 
    public ArrayList<ArrayList<Integer>> subsetsWithDup(int[] num) {
        if (num == null || num.length <= 0)
            return listAll;
        ArrayList<Integer> list = new ArrayList<>();
        Arrays.sort(num); 
        Findsubset(num, 0, list);      
        return listAll;
    }
 
    public void Findsubset(int[] set, int start, ArrayList<Integer> list) {
        listAll.add(new ArrayList<>(list)); 
        //在某个位置选个一个数 从下标start开始选择
        for (int i = start; i < set.length; i++) {
            //i > start 重复序列 第一个可以放进去 其他不放
            //重复序列的首个加入 后面重复的才有机会加入
            //首个 不加入 后边都不加入
            //这样保证只考虑在此位置 只放首个元素，其他重复元素不放在此位置。后面的要加入，则在下一位置
            if (i > start && set[i] == set[i - 1])
                continue;
            list.add(set[i]);
            Findsubset(set, i + 1, list);
            list.remove(list.size() - 1);
        }
    }
}

```

# 法2
```java
 public  ArrayList<ArrayList<Integer>> subsets(int[] S) {
        ArrayList<ArrayList<Integer>> res = new ArrayList<>();
        Arrays.sort(S);
        helperDupli(S,0,true,new ArrayList<>(),res);
        return  res;
    }
private void helperDupli(int[] s, int curIndex,boolean taken, ArrayList<Integer> cur, ArrayList<ArrayList<Integer>> res) {
        if(curIndex == s.length){
            res.add(new ArrayList<>(cur));
        }else{

            //CurIndex处的 s元素不加入集合内
            helperSub(s,curIndex+1,cur,res);
            //taken 为true表示上一个curIndex处元素，加入了。此时，此处若是重复元素，他有加入的机会。不是重复的元素更有机会
            //taken false 表示上一个curIndex处元素，不加入。此时，此处若是重复元素，不能加入。即两个条件都不满足。。
            //若不是重复元素 可以加入
            if(taken ||s[curIndex-1]  != s[curIndex]){
                //curIndex 处 s元素加入集合内
                cur.add(s[curIndex]);
                helperSub(s,curIndex+1,cur,res);
                cur.remove(cur.size()-1);
            }
        }
    }
```