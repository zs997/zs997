---
layout:     post
title: Leecode
subtitle:    LeetCode78 subsets1
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
现在有一个没有重复元素的整数集合S，求S的所有子集
注意：
你给出的子集中的元素必须按非递增的顺序排列
给出的解集中不能出现重复的元素
例如：
如果S=[1,2,3], 给出的解集应为：
[↵  [3],↵  [1],↵  [2],↵  [1,2,3],↵  [1,3],↵  [2,3],↵  [1,2],↵  []↵]

# 分析
* 每个元素都要选择加入不加入集合的机会。
* 所以可以使用回溯法，每个位置可以是空，可以是该位置的元素。

# java 代码
```java
import java.util.*;
public class Solution {
    public  ArrayList<ArrayList<Integer>> subsets(int[] S) {
       
        ArrayList<ArrayList<Integer>> res = new ArrayList<>();
        if(S == null || S.length == 0){
            return res;
        }
        Arrays.sort(S);
        helperSub(S,0,new ArrayList<>(),res);
        
         Collections.sort(res, new Comparator<ArrayList<Integer>>() {
          @Override
            public int compare(ArrayList<Integer> o1, ArrayList<Integer> o2) {
                if (o1.size()!=o2.size()) {
                    return o1.size()-o2.size();
                }else {
                    for (int i = 0; i < o1.size(); i++) {
                        int comp=o1.get(i)-o2.get(i);
                        if (comp!=0) return comp;
                    }
                }
                return 0;
            }
        });
        return  res;
    }
    
    private void helperSub(int[] s, int curIndex, ArrayList<Integer> cur, ArrayList<ArrayList<Integer>> res) {
        if(curIndex == s.length){
            res.add(new ArrayList<>(cur));
        }else{
            //CurIndex处的 s元素不加入集合内
            helperSub(s,curIndex+1,cur,res);
            
            //curIndex 处 s元素加入集合内
            cur.add(s[curIndex]);
            helperSub(s,curIndex+1,cur,res);
            cur.remove(cur.size()-1);
        }
    }
}
```
# 法二

```java
import java.util.*;
 
public class Solution {
    ArrayList<ArrayList<Integer>> listAll = new ArrayList<>();
 
    public ArrayList<ArrayList<Integer>> subsets(int[] num) {
        if (num == null || num.length <= 0)
            return listAll;
        ArrayList<Integer> list = new ArrayList<>();
        Arrays.sort(num);
 
        Findsubset(num, 0, list);
           //排序
        Collections.sort(listAll, new Comparator<ArrayList<Integer>>() {
          @Override
            public int compare(ArrayList<Integer> o1, ArrayList<Integer> o2) {
                if (o1.size()!=o2.size()) {
                    return o1.size()-o2.size();
                }else {
                    for (int i = 0; i < o1.size(); i++) {
                        int comp=o1.get(i)-o2.get(i);
                        if (comp!=0) return comp;
                    }
                }
                return 0;
            }
        });
        return listAll;
    }
 
    public void Findsubset(int[] set, int start, ArrayList<Integer> list) {
        listAll.add(new ArrayList<>(list));
 
        for (int i = start; i < set.length; i++) {
            list.add(set[i]);
            Findsubset(set, i + 1, list);
            list.remove(list.size() - 1);
        }
    }
}
```