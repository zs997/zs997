---
layout:     post
title: Leecode
subtitle:     palindrome-number
date:       2020-03-8
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
在不使用额外的内存空间的条件下判断一个整数是否是回文
提示：
负整数可以是回文吗？（比如-1）
如果你在考虑将数字转化为字符串的话，请注意一下不能使用额外空间的限制
你可以将整数翻转。但是，如果你做过题目“Reverse Integer”，你会知道将整数翻转可能会出现溢出的情况，你怎么处理这个问题？
这道题有更具普遍性的解法。
# 分析
* 负数不是回文
* 对于可能是回文的数字这样判断：
	* 设置一个div变量，和要判断的数保持位数相同，最高位为1，其他位为0，如 判断num=8428时，div := 1000。
	* 这时判断 8428/div = 8（最高位） 和 8421%10 = 8（最低位） 是否相等，如果不相等，直接返回false。否则，将数字 num = 8428 变成 42，div变成10，继续判断.....

# java 代码
```java
public class Solution {
    public boolean isPalindrome(int x) {
         if(x < 0){
            return false;
        }
        int div = 1;
       while(x/div >= 10){
           div  = div *10;
       }
        int num = x;
       int left = 0;
        int right = 0;
       while(div != 0){
           left = num/div;
           right = num%10;
           if(left != right){
               return false;
           }          
           num = (num - left*div)/10;
            div = div /100;
       }
        return true;
         
    }
}
```