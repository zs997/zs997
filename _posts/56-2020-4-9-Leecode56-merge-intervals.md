---
layout:     post
title: Leecode
subtitle:    Leecode56 merge-intervals
date:       2020-04-10
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
给出一组区间，请合并所有重叠的区间。
例如，
给出[1,3],[2,6],[8,10],[15,18],
返回[1,6],[8,10],[15,18].

# java 代码
```java 
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
import java.util.ArrayList;
import java.util.Arrays;
public class Solution {
    public ArrayList<Interval> merge(ArrayList<Interval> intervals) {
        ArrayList<Interval> res = new ArrayList<>();
        if(intervals == null){
            return res;
        }
        int start [] = new int[intervals.size()];
        int end [] = new int[intervals.size()];        
        for(int i = 0; i < intervals.size(); i++){
            //将所有的线段起点终点保存
            start[i] = intervals.get(i).start;
            end[i] = intervals.get(i).end;
        }  
        //将所有起点终点排序，等价新的线段组合
        Arrays.sort(start);
        Arrays.sort(end);
        int i = 0;
        while(i < start.length){
            //记录起点
            int s = start[i];
            //当前线段的末尾 如果能包含下一个线段 一直移动i
            while(i < start.length-1&& end[i] >= start[i+1]){
                i++;
            }
            int e = end[i];
            res.add(new Interval(s,e));
            i++;
        }
        return res;
    }
}
```