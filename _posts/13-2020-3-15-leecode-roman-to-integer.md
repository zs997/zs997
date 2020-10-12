---
layout:     post
title: Leecode
subtitle:     roman-to-integer
date:       2020-03-15
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
请将给出的罗马数字转化为整数
保证输入的数字范围在1 到 3999之间。
# 分析
都加起来，找出反作用的，减二倍。
# java代码
```java
public class Solution {
    public int romanToInt(String s) {
        if(s == null || s.length() == 0){return 0; }
        int res = 0;
        if(s.indexOf("CM") != -1) res -= 200;
         if(s.indexOf("CD") != -1) res -= 200;
         if(s.indexOf("XC") != -1) res -= 20;
         if(s.indexOf("XL") != -1) res -= 20;
         if(s.indexOf("IX") != -1) res -= 2;
         if(s.indexOf("IV") != -1) res -= 2;
        
        for(char c : s.toCharArray()){
            if(c == 'M'){
                 res += 1000;
            }else if(c == 'D'){
                res += 500;
            }else if(c == 'C'){
                res += 100;
            }else if(c == 'L'){
                res += 50;
            }else if(c == 'X'){
                res += 10;
            }else if(c == 'V'){
                res += 5;
            }else if(c == 'I'){
                res += 1;
            }
        }
        return res;
    }
}
```