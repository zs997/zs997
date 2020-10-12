---
layout:     post
title: Leecode
subtitle:    Leecode44 wildcard-matching
date:       2020-04-07
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---

# 题目描述
请实现支持'?'and'*'.的通配符模式匹配
'?' 可以匹配任何单个字符。↵'*' 可以匹配任何字符序列（包括空序列）。↵↵匹配应该覆盖整个输入字符串（而不是部分）。↵函数声明为：↵bool isMatch(const char *s, const char *p)↵↵下面给出一些样例：↵isMatch("aa","a") → false↵isMatch("aa","aa") → true↵isMatch("aaa","aa") → false↵isMatch("aa", "*") → true↵isMatch("aa", "a*") → true↵isMatch("ab", "?*") → true↵isMatch("aab", "c*a*b") → false

# 分析

* 使用动态规划算法，设置一个二维布尔数组，match[s.length+1][p.length+1 ],match[si][pi] 表示，s串的前si子串和pi串的前j子串是否通配符模式匹配。
#### 初始化
* match[0][0]，两个空串，匹配。
* match[1~s.length][0]，表示通配符模式是空串，那么其他正常字符串都不与之匹配。
* match[0][1~p.length]，表示通配符模式不是空串，用它能否匹配空串。而通配符模式串能匹配空串的可能性只有出现'\*'字符的情况。出现 \* 字符时，如果要匹配空字符，这时 match[0][pi] = match[0][pi-1];只需将此字符（\*）去掉，看能否匹配空串。
*把可能出现true的操作考虑一遍， 以上可以完成初始化操作。
#### 递推状态
*  s[si-1] != p[pi-1] (s字符串中第si个元素，p字符串中第pi个元素不相等)，match[si][pi] 为false， 无需改变，因为初始化是false。
* s[si-1] == p[pi-1]  或者  p[pi-1]=='?') （s字符串中第i个元素，p字符串中第j个元素相等，或者匹配了'?'），此时当前位置是匹配的，就看各自去掉一位，是否匹配。 match[si][pi] = match[si-1][pi-1];
* p[pi-1] == '\*' ,如果匹配了 '\*' ,可以将其认为是空字符，match[si][pi] = match[si][pi]。
   同时，可以认为匹配了S[si]位置的字符，而且匹配好之后，‘\*’的魔力没有变化，还可以继续用。所以：match[si][pi] = match[si-1][pi]；
   将以上两情况合并：
			 match[si][pi] = match[si-1][pi]||match[si][pi-1];
# java代码
```java
public class Solution {
    public boolean isMatch(String s, String p) {
        if(s == null || p == null){
            return false;
        }
        boolean match[][] = new boolean[s.length()+1][p.length()+1];
        match[0][0] = true;
        for(int pi = 1; pi <= p.length();pi++){
            if(p.charAt(pi-1) == '*'){
                match[0][pi] = match[0][pi-1];
            }
        }
        
        for(int si = 1; si <= s.length();si++){
            for(int pi = 1; pi <= p.length();pi++){
                if((p.charAt(pi-1) == s.charAt(si-1))||(p.charAt(pi-1)=='?')){
                    match[si][pi] = match[si-1][pi-1];
                }else if(p.charAt(pi-1) == '*'){
                    match[si][pi] = match[si-1][pi]||match[si][pi-1];
                }
            }
        }
        
        return match[s.length()][p.length()];
    }
}
```