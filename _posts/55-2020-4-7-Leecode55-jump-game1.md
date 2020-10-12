---
layout:     post
title: Leecode
subtitle:    Leecode55 jump-game
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
给出一个非负整数数组，你最初在数组第一个元素的位置

数组中的元素代表你在这个位置可以跳跃的最大长度
判断你是否能到达数组最后一个元素的位置
例如
A =[2,3,1,1,4], 返回 true.

A =[3,2,1,0,4], 返回 false.

# 分析
* 遍历数组，判断基于此点，最远能到哪个位置，更新最远能到的位置maxReach，maxReach是当前已知的最远位置。
* 再遍历过程中，如果索引超出了当前的maxReach,则不能继续遍历。
* 遍历结束后，如果maxReach 超出了 数组的最大索引，说明可以通过某种方式跳到最后一个元素，否则无法跳到。
# java 代码 
```java
import java.lang.Math;
public class Main {
    public boolean canJump(int[] A) {
        if(A == null||A.length < 2){return true;}
        int i = 0;
        int maxReach = 0;
        for(i = 0; i < A.length && i <= maxReach; i++){
            maxReach = Math.max(maxReach,A[i]+i);          
        }
        if(maxReach < A.length-1){ return false;}
        return true;     
    } 
}
```