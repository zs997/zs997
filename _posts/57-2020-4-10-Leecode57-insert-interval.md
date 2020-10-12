---
layout:     post
title: Leecode
subtitle:    Leecode57 insert-interval
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
给定一组不重叠的时间区间，在时间区间中插入一个新的时间区间(如果有重叠的话就合并区间)。
这些时间区间初始是根据它们的开始时间排序的。
示例1:
给定时间区间[1,3]，[6,9]，在这两个时间区间中插入时间区间[2,5]，并将它与原有的时间区间合并，变成[1,5],[6,9].
示例2：
给定时间区间[1,2],[3,5],[6,7],[8,10],[12,16],在这些时间区间中插入时间区间[4,9]，并将它与原有的时间区间合并，变成[1,2],[3,10],[12,16].
这是因为时间区间[4,9]覆盖了时间区间[3,5],[6,7],[8,10].
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
import java.util.*;
public class Solution {
    public ArrayList<Interval> insert(ArrayList<Interval> intervals, Interval newInterval) {
        ArrayList <Interval> res = new ArrayList<>();
        if(intervals == null){
            return res;
        }
        int i =0;
        int n = intervals.size();
        int start = newInterval.start;
        int end = newInterval.end;
       //不能取等号，这是把 newInterval 之前的所有都放进res
        while(i < n && intervals.get(i).end < start){
            res.add(intervals.get(i));      
            i++;
        }
        //存在一种情况 newInterval在这些线段之后
        if(i == n){
            res.add(newInterval);
            return res;
        }
        //到这一步 说明 newInterval 有一个合适的融合位置
        start = Math.min(start,intervals.get(i).start);
        //待插入线段的end坐标 
        int endn = end;
        while(i < n && intervals.get(i).start <= endn){
            end = Math.max(end,intervals.get(i).end);
            i++;
        }        
        res.add(new Interval(start,end));
        //将右侧剩余的加入
        while(i < n){
            res.add(intervals.get(i));
            i++;
        }
        return res;
        
    }
}
```