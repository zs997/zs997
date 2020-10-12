---
layout:     post
title: Leecode
subtitle:    implement-strstr
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
实现函数 strStr。
函数声明如下：
char *strStr(char *haystack, char *needle)
返回一个指针，指向needle第一次在haystack中出现的位置，如果needle不是haystack的子串，则返回null。
# 分析
暴力破解
# java 代码
```java
public class Solution {
    public String strStr(String haystack, String needle) {
        if(haystack == null || needle == null || needle.length() ==0){
            return haystack;
        }
        if(haystack.length() < needle.length()){
            return null;
        }
        for(int i = 0; i< haystack.length();i++){
            int j = i;
            int k = 0;
            while(j < haystack.length()&& k < needle.length() &&haystack.charAt(j) == needle.charAt(k)){
                j++;
                k++;                
            }
            if(k >=  needle.length()){
                return haystack.substring(i);
            }
        }
        return null;
    }
}
```