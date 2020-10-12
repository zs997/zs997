---
layout:     post
title: Leecode
subtitle:     generate-parentheses
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
给出n对括号，请编写一个函数来生成所有的由n对括号组成的合法组合。
例如，给出n=3，解集为：
"((()))", "(()())", "(())()", "()(())", "()()()"

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

"((()))", "(()())", "(())()", "()(())", "()()()"
# 分析
这题略难
# java 代码
```java
import java.util.*;
public class Solution {
    public ArrayList<String> generateParenthesis(int n) {
        ArrayList <String> res = new ArrayList<>();
        helper("",res,n,0,0);
        return res;
    }
    public void helper(String cur, ArrayList<String> res,int n , int left, int right){
        if(right == n){
            //到节点了
            res.add(cur);
            return;
            
        }else{
            if(left < n){
                helper(cur + "(",res,n,left+1,right);
            }
            if(right < left){
                helper(cur + ")",res,n,left,right+1);
            }
        }
    }
}
```