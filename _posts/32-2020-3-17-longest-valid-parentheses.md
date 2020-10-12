---
layout:     post
title: Leecode
subtitle:    longest-valid-parentheses
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
给出一个仅包含字符'('和')'的字符串，计算最长的格式正确的括号子串的长度。
对于字符串"(()"来说，最长的格式正确的子串是"()"，长度为2.
再举一个例子：对于字符串")()())",来说，最长的格式正确的子串是"()()"，长度为4.

# 分析
* 使用栈存放‘（’的下标，遍历输入的字符。遇到 '(' 入栈，遇到‘）’出栈。
* 用 leftmost 指向 当前检查的合法括号序列 前一个下标。
* 遍历输入字符，下标为index，遇到‘（’入栈时：
	*	将下标入栈。 
* 遍历输入字符，下标为index，遇到‘）’出栈时：
	* 如果栈状态为空，则说明没有匹配的（，leftmost = index ，表明要检查下一组括号。
	* 如果栈不为空，则说明可以匹配。出栈。
		* 如果此时栈顶不为空，则当前合法括号范围是  index - peek，更新最大值。
		* 如果此时栈顶为空，则当前合法括号范围是  index - leftmost，更新最大值。
# java代码
```java
import java.util.*;

public class Solution {
    public int longestValidParentheses(String s) {
        if(s == null || s.length() <= 1){return 0;}
        
        char arr [] = s.toCharArray();
        int max = 0;
        int index = 0;
        int leftmost = -1;
        
        //装放下标
        Stack <Integer> stack = new Stack<>();
        for(; index < arr.length; index++){
            if(arr[index] == '('){
                stack.push(index);
            }else{
                // ) 情况
                if(!stack.isEmpty()){
                    //出栈
                    int temp = stack.pop();
                    if(!stack.isEmpty()){
                        max = Math.max(index - stack.peek(),max);
                    }else{
                        max = Math.max(index - leftmost,max);
                    }
                }else{
                    leftmost = index;
                }
            }
        }
        
        return max;
    }
}
```