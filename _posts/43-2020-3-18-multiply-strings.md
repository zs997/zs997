---
layout:     post
title: Leecode
subtitle:    multiply-strings
date:       2020-03-18
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---

# 题目描述
给出两个用字符串表示的数字，将两个数字的乘积作为字符串返回。
备注：数字可以无限大，且是非负数。
# java 代码
```java
public class Solution {
public String multiply(String num1, String num2) {
        if(num1 == null || num2 == null || num1.length()==0||num2.length() == 0){
            return "0";
        }
        int len1 = num1.length();
        int len2 = num2.length();
        int res [] = new int [len1+len2];
        for(int i = len1 - 1; i >= 0; i--){
            for(int j = len2 - 1; j >= 0;j--){
                int multi = (num1.charAt(i)-'0')*(num2.charAt(j)-'0');
                int low = i+j+1;
                int high = i+j;
                multi += res[low];
                int base = multi % 10;
                int carry = multi / 10;
                res[low] = base;
                res[high] += carry;
              }
        }
        StringBuffer sb = new StringBuffer();
        for(int i : res){
            // i != 0 时 可以放入  
            // i == 0 时 只要之前放入过其他元素就行 如 10是合法的
            //只有 0开头跳过
            if((sb.length() != 0)||(i != 0)){
                sb.append(i);
            }            
            /*
            没有sb放过元素，开头不能放入0
             if(！(sb.size() == 0)&&(i == 0)){                
            }            
            */
        }
        return sb.length() == 0 ? "0":sb.toString();
    }
}
```