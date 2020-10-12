---
layout:     post
title: Leecode
subtitle:    LeetCode87-scramble-string
date:       2020-04-18
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---

# 题目描述
题目给出一个字符串s1，我们可以用递归的方法将字符串分成两个非空的子串来将s1表示成一个二叉树
下面是s1=“great”的一种二叉树的表现形式：
    great↵   /    ↵  gr    eat↵ /     /  ↵g   r  e   at↵           / ↵          a   t
将字符串乱序的方法是：选择任意的非叶子节点，交换它的两个孩子节点。
例如：如果我们选择节点“gr”交换他的两个孩子节点，就会产生一个乱序字符串"rgeat".
    rgeat↵   /    ↵  rg    eat↵ /     /  ↵r   g  e   at↵           / ↵          a   t
我们称"rgeat"是"great"的一个乱序字符串。
类似的：如果我们继续交换“eat”的两个孩子节点和“at”的两个孩子节点，会产生乱序字符串"rgtae".
    rgtae↵   /    ↵  rg    tae↵ /     /  ↵r   g  ta  e↵       / ↵      t   a
我们称"rgtae"是"great"的一个乱序字符串。
给出两个长度相同的字符串s1 和 s2，请判断s2是否是s1的乱序字符串。

# java 代码
```java
import java.util.*;
public class Solution {
    public boolean isScramble(String s1, String s2) {
        if(s1 == null || s2 == null || s1.length()!= s2.length()){
            return false;
        }
        if(s1.length() == 1 && s1.equals(s2)){
            return true;
        }
        char [] ch1 = s1.toCharArray();
        char [] ch2 = s2.toCharArray();
        Arrays.sort(ch1);
        Arrays.sort(ch2);
        String str1 = new String(ch1);
        String str2 = new String(ch2);
        if(!str1.equals(str2)){
            return false;
        }
        
        for(int i =1;i <s1.length();i++){
            String s1Left = s1.substring(0,i);
            String s1Right = s1.substring(i,s1.length()); 
            if( (isScramble(s1Left,s2.substring(0,i)) && isScramble(s1Right,s2.substring(i,s2.length())))||
              (isScramble(s1Left,s2.substring(s2.length()-i,s2.length())) && isScramble(s1Right,s2.substring(0,s2.length()-i)))){
                return true;
            }
        }        
        return false;       
    }
}
```