---
layout:     post
title: Leecode
subtitle:    regular-expression-matching
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
请实现支持'.'and'*'.的通配符模式匹配
'.' 可以匹配任何单个字符。↵'*' 可以匹配任何字符序列（包括空序列）。↵↵匹配应该覆盖整个输入字符串（而不是部分）。 ↵函数声明为：↵bool isMatch(const char *s, const char *p)↵↵下面给出一些样例：↵isMatch("aa","a") → false↵isMatch("aa","aa") → true↵isMatch("aaa","aa") → false↵isMatch("aa", "a*") → true↵isMatch("aa", ".*") → true↵isMatch("ab", ".*") → true↵isMatch("aab", "c*a*b") → true
# 分析
一言难尽
# java 代码
```java
public class Solution {
    public boolean isMatch(String s, String p) {
        if(s == null || p == null){
            return false;
        }
        //默认值都是false 只需将可能是true的填写上
        boolean [][] match = new boolean [p.length()+1][s.length()+1];
        match[0][0] = true;
        for(int pi = 1;pi <= p.length();pi++){
            if(p.charAt(pi-1)=='*'){
                match[pi][0] = match[pi-2][0]; 
            }
        }
        for(int sj = 1 ;sj <= s.length(); sj++){
            for(int pj = 1; pj <= p.length(); pj++){
                if(p.charAt(pj-1)=='.' || p.charAt(pj-1)==s.charAt(sj-1)){
                    match[pj][sj] = match[pj-1][sj-1];
                }else if(p.charAt(pj-1)=='*'){
                    if(p.charAt(pj-2) == s.charAt(sj-1) || p.charAt(pj-2)=='.'){
                        match[pj][sj] = match[pj-2][sj] || match[pj][sj-1];
                    }else{
                        match[pj][sj] = match[pj-2][sj];
                    }
                }
            }
        }
        
        return match[p.length()][s.length()];
    }
}
```