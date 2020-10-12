---
layout:     post
title: Leecode
subtitle:    longest-substring-without-repeating-characters
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
给定一个字符串，找出最长的不具有重复字符的子串的长度。例如，“abcabcbb”不具有重复字符的最长子串是“abc”，长度为3。对于“bbbbb”，最长的不具有重复字符的子串是“b”，长度为1。

# 分析
使用快慢指针指示不重复的子串，重复判断查询布尔型的数组。如果没有重复，右指针一直向前移动。一旦重复，记录此时产生的子串长度，更新最长子串。并且使左指针移动至与右指针重复的位置，并从下一个位置作为新串的起点。将重复记录删除。右指针继续向前移....如此往复

# java代码
```java
public class Solution {
        public int lengthOfLongestSubstring(String s) {
          if(s == null || s.equals("")){
            return 0;
        }
        char[] arr = s.toCharArray();
        int left = 0;
        int right = 0;
        int max = 0;
        boolean visited []  = new boolean[128];
        while(right < arr.length ){
            if(visited[(int)arr[right]] == false){
                visited[(int)arr[right]] = true;
                right++;
            }else{
                max = Math.max(max,right - left);
                while (left < right && arr[right] != arr[left]){
                    visited[(int)arr[left]] = false;
                    left ++;
                }
                left++;
                right++;
            }
        }
        max = Math.max(max,right - left);
        return max;
        }
}
```