---
layout:     post
title: Leecode
subtitle:    letter-combinations-of-a-phone-number
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
给出一个仅包含数字的字符串，给出所有可能的字母组合。
数字到字母的映射方式如下:(就像电话上数字和字母的映射一样)
![](https://img-blog.csdnimg.cn/20200315223337792.png)
Input:Digit string "23"Output:["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
注意：虽然上述答案是按字典序排列的，但你的答案可以按任意的顺序给出
# 分析
* 深度优先搜索
* 遍历
# java 代码
```java
import java.util.*;
public class Solution {
    public ArrayList<String> letterCombinations(String digits) {
        ArrayList <String> res = new ArrayList<String>();
        if(digits == null || digits.length() == 0){
            res.add("");
            return res;
        }
        HashMap <Character,char []> map = new HashMap<>();
        map.put('2',new char[]{'a','b','c'});
        map.put('3',new char[]{'d','e','f'});
        map.put('4',new char[]{'g','h','i'});
        map.put('5',new char[]{'j','k','l'});
        map.put('6',new char[]{'m','n','o'});
        map.put('7',new char[]{'p','q','r','s'});
        map.put('8',new char[]{'t','u','v'});
        map.put('9',new char[]{'w','x','y','z'});
        helper("",0,digits,res,map);
        
        return res;
    }
    
    public void  helper(String curr,int currIndex,String digits,ArrayList<String> res,HashMap<Character,char []> map){
        if(currIndex == digits.length()){
            res.add(curr);
        }else{
            char c = digits.charAt(currIndex);
            if(map.containsKey(c)){
                for(char cc : map.get(c)){
                    helper(curr+cc,currIndex+1,digits,res,map);
                }
            }
        }
    }
}
```