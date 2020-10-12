---
layout:     post
title: Leecode
subtitle:    Leecode49 anagrams
date:       2020-04-08
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---

# 题目描述
给出一个字符串数组，返回所有互为“换位词（anagrams）”的字符串的组合。（换位词就是包含相同字母，但字母顺序可能不同的字符串）
备注：所有的输入都是小写字母
例如：
输入["tea","and","ate","eat","den"]
返回
[↵  ["ate", "eat","tea"],↵  ["and","den"]↵]
# 分析
* 互为换位词有一个共同点，他们包含相同字母，它们的字母排序就一致了。
* 可设置一个map，key是字母的排序，value是一个List\<String\>，用来装带有相同排序的字符串。
* 题目要求找出互为换位词的组合，只有一个词跳过。
# java 代码
```java 
import java.util.*;
public class Solution {
    public ArrayList<String> anagrams(String[] strs) {
        ArrayList<String> res = new ArrayList<>();
        if(strs == null || strs.length == 0){
            return res;
        }
        Map<String,ArrayList<String>> map = new HashMap<String,ArrayList<String>>();
        for(String s : strs){
            String key = sortString(s);
            if(!map.containsKey(key)){
                ArrayList<String> list = new ArrayList<>();
                map.put(key,list);
            }
            map.get(key).add(s);
        }
        Set<String> strings = map.keySet();
        for(String key : strings){
            ArrayList<String> list = map.get(key);
            if(list.size() > 1){
                res.addAll(list);
             }
        }        
        return res;       
    }
    
    public String sortString(String s){
        char []  strArr = s.toCharArray();        
        Arrays.sort(strArr);
        return new String(strArr);
    }
}
```