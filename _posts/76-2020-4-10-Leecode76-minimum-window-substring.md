---
layout:     post
title: Leecode
subtitle:    Leecode76 minimum-window-substring
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
给出两个字符串S和T，要求在O（n）的时间复杂度内在S中找出最短的包含T中所有字符的子串。
例如：
S ="ADOBECODEBANC"
T ="ABC"
找出的最短子串为"BANC".
注意：
如果S中没有包含T中所有字符的子串，返回空字符串 “”；
满足条件的子串可能有很多，但是题目保证满足条件的最短的子串唯一。
# java 代码
```java
public class Solution {
    int tArr[] = new int[256];
    public String minWindow(String S, String T) {
        if(S==null||T == null || S.length() == 0 || T.length()==0){
            return "";
        }
        int matchCount = 0;
        int count = 0;
        String res = "";
        //tArr初始化之后不改变        
        for(char ch : T.toCharArray()){
            //统计 T中各字符数量
            tArr[ch]++;
            count++;
        }
        int sArr[] = new int [256];
        int left = 0;
        int right = 0;
        //从某一下标开始（包括），在S中找到下一个符合T的字符下标。
        left = findNextT(0,S);
        //没有符合T的字符
        if(left == S.length()){
            return "";
        }
        right = left;
        while(right < S.length()){
            //如果没加满           
            if(sArr[S.charAt(right)] < tArr[S.charAt(right)]){
                matchCount++;
            }
            //可能会匹配了多余的
             sArr[S.charAt(right)]++;
            //符合条件的
            while(right < S.length() && matchCount == count){
                //更新最小
                if(res == "" || res.length() > right - left +1){
                    res = S.substring(left,right+1);
                }
                //left右移  只有不满了 才要减小匹配数
                if(sArr[S.charAt(left)] <= tArr[S.charAt(left)]){
                    matchCount --;
                }
                sArr[S.charAt(left)]--;
                left = findNextT(left+1,S);                
            }
          right = findNextT(right+1,S);         
        }
        return res;
    }
    public int findNextT(int start,String s){
        if(start >= s.length()){
            return s.length();
        }
        while(start < s.length()){
            //tArr 里面有此数
            if(tArr[s.charAt(start)] != 0){
                return start;
            }
            start ++;
        }
        return start;
    }
}
```