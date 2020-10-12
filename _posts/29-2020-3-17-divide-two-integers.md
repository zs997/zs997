---
layout:     post
title: Leecode
subtitle:    divide-two-integers
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
在不使用乘法运算符，除法运算符和取余运算符的情况下对两个数进行相除操作
Divide two integers without using multiplication, division and mod operator.

# 分析
* 使用移位操作，将除数左移一定位数，直到大于被除数。
* 由于记录了左移的位数n，那么将1 左移n-1位，就是每一次被除数除以除数，所得的结果。将其记录。
*  将被除数减去 除数 << n-1  得到新的被除数，继续左移判断。
* 当被除数小于除数时，可以得出最后结果。
# java代码
```java
public class Solution {
    public int divide(int dividend, int divisor) {
        if(divisor == 0) {
            if(dividend < 0){
                return Integer.MIN_VALUE;
            }else{
                return Integer.MAX_VALUE;
            }
        }
        if(dividend == Integer.MIN_VALUE){
            if(divisor == 1){
                return dividend;
            }else if (divisor == -1){
                return Integer.MAX_VALUE;
            }
        }
        long divd = (long) dividend;
        long divs = (long) divisor;
        //变号
        int sign = 1;
        if(divd < 0){
            sign = -sign;
            divd = -divd;
        }
        if(divs < 0){
            sign = -sign;
            divs = -divs;
        }
        
        int res = 0;
        while(divd >= divs){
            int shift = 0;        
            while(divd >= divs << shift){
                shift ++ ;
            }
            divd -= (divs << (shift-1));
            res += (1 << (shift-1));
        }
        return sign*res;
        
        
    }
}
