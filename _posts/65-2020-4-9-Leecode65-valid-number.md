---
layout:     post
title: Leecode
subtitle:    Leecode65 valid-number
date:       2020-04-09
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---

# 题目描述
判断给出的字符串是否是数字
一些例子：
"0"=>true
" 0.1 "=>true
"abc"=>false
"1 a"=>false
"2e10"=>true
注意：
这道题故意陈述的比较模糊，在实现一个需求之前，你应该预先收集所有的要求。
# java 代码
```java
public class Solution {
    public boolean isNumber(String s) {
        if(s == null || s.length() == 0){
            return false;
        }
        //数值可能的情况
        //   +-xxx.xxxe+-xxx   
        //可以将E前后分为两部分，如果有e，后面必须跟数字
        //如果没有e 前面的数字必须符合小数要求
        int i = 0;
        int n = s.length();
        //flag[0] : 表示第一块数字的状态 -1 -> 没有数字  0 ： 不符合数字 1：符合数字
        //flag[1] : 表示第二块数字的状态 -1 -> 没有数字  0 ： 不符合数字 1：符合数字
        int flag [] = {-1,-1};
        //跳过前面可能的空格
        while(i < n && Character.isWhitespace(s.charAt(i))){
            i++;
        }       
        //********************************判断e之前的数字*******************************************************************************
        //跳过正负号
        if(i < n && ((s.charAt(i) == '+' )||(s.charAt(i) == '-'))){
            i++;
        }
        //接下来必须是数字了   xxx.xxx 可以的  xxx. .xxx 都可以 
        //也就是说  可以直接跳过一次小数点 剩下全要是数字
        flag[0] = 0;
        while(i < n && Character.isDigit(s.charAt(i))){
            i++;          
            flag[0] = 1;
        }
        //如果有小数点 
        if(i < n && s.charAt(i) == '.'){
            i++;          
           //  flag[0] = 0;
            while(i < n && Character.isDigit(s.charAt(i))){
                i++;              
                flag[0] = 1;
            }
        }
      //************************************************************************************************************************
      //******************************************判断e和对应的指数******************************************************************************          
        //判断可能出现e
        if(i < n && s.charAt(i) == 'e'){
            i++;
            //正负指数
            if(i < n && ((s.charAt(i) == '+' )||(s.charAt(i) == '-'))){
                i++;
            }
            flag[1] = 0;           
            while(i < n && Character.isDigit(s.charAt(i))){
                i++;              
                flag[1] = 1;
            }            
        }
        //**************************************************************************************************************************
        //跳过后面可能的空格
        while(i < n && Character.isWhitespace(s.charAt(i))){
            i++;
        }       
        //**************************************判断结果***********************************************************************************
        if(i == n ){
            //
            if(flag[1] == -1 ||flag[1] == 1){
                //第二块数字符合或者不存在第二块，最终结果取决于第一块
                return flag[0] == 1?true:false;
            }else{
                // flag[1] == 0 说明第二块数字不符合
                return false;
            }           
        }
        return false;        
    }
}
```