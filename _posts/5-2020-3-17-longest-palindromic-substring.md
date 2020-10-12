---
layout:     post
title: Leecode
subtitle:     longest-palindromic-substring
date:       2020-03-17
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---
# 题目描述
找出给出的字符串S中最长的回文子串。假设S的最大长度为1000，并且只存在唯一解。
# 分析
* 使用动态规划算法。pali[i][j] 代表从i下标到j下标的子串是否是回文。
* 一个字符肯定是回文，两个字符如果一样，也是回文，进而初始化。
* 以此考虑三个字符，四个字符.....n个字符。
* 如果在某次计算时，arr[i] == arr[i+n] 那么如果pili[i+1][i+n-1]是回文的话，整体也是回文。
# java 代码
```java
public class Solution {
    public String longestPalindrome(String s) {
        if(s == null || s.length() <= 1 )    return s;
        
       
        char [] arr = s.toCharArray();
        int len = arr.length;
        int start = 0;
        int length = 1;
        boolean pali [][] = new boolean [len][len];
        
        for(int i = 0; i < pali.length; i++){
            pali[i][i] = true;
           // length = 1;
        }
        
        for(int i = 0; i < arr.length-1; i++){
            if(arr[i] == arr[i+1]){
                pali[i][i+1] = true;                
                start = i;
                length = 1;
            }
        }
        
        for(int n = 2; n < len; n++){
            for(int i = 0; i+n  < len; i++){
                if(arr[i] == arr[i+n] && pali[i+1][i+n-1]){
                    pali[i][i+n] = true;
                    start = i;
                    length = n;
                }
            }
        }
        
        return s.substring(start,start+length+1);
        
    }
}
```