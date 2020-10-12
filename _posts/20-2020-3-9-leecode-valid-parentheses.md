---
layout:     post
title: Leecode
subtitle:   valid-parentheses
date:       2020-03-09
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
给出一个仅包含字符'(',')','{','}','['和']',的字符串，判断给出的字符串是否是合法的括号序列
括号必须以正确的顺序关闭，"()"和"()[]{}"都是合法的括号序列，但"(]"和"([)]"不合法。
# 分析
* 使用栈结构，在遍历字符的时候，如果是正括号，压栈，如果是反括号，弹出一个栈顶元素，判断是否和反括号匹配。如果匹配继续，反之是不合法的。最后如果栈被清空了，说明所有元素都匹配，则是合法序列。
# java代码
```java
public class Solution {
    public boolean isValid(String s) {
        if(s == null || s.equals("")){return false;}    
        char [] data = s.toCharArray();
        Stack<Character> stack = new Stack<>();        
        for(int i = 0; i < data.length; i++){
            if(isForward(data[i])){
                stack.push(data[i]);
            }else{
                if(stack.isEmpty()){
                    return false;
                }else{
                    char temp = stack.pop();
                    if(!isMatch(temp,data[i])){
                        return false;
                    }
                }
            }
        }
        if(stack.isEmpty()){
            return true;
        }else{
            return false;
        }        
    }
    public boolean isMatch(char a,char b){
        if( (a=='('&& b==')')||(a=='{'&&b=='}')|| (a=='['&&b==']')){
            return true;
        }
        return false;
    }
    public boolean isForward(char c){
        if(c =='('||c =='{'||c =='['){
            return true;
        }
        return false;
    }
}
```