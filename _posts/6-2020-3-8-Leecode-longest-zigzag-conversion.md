---
layout:     post
title: Leecode
subtitle:    zigzag-conversion
date:       2020-03-8
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - leecode
---
# 题目描述
字符串"PAYPALISHIRING"写成3行的Z字形的样式如下：

	P   A   H   N↵A P L S I I G↵Y   I   R

按行读这个Z字形图案应该是 "PAHNAPLSIIGYIR"

请编写代码完成将字符串转化为指定行数的Z字形字符串：

	string convert(string text, int nRows);

	convert("PAYPALISHIRING", 3)应该返回"PAHNAPLSIIGYIR"
# 分析
使用stringbuilder数组，维度为nRows，数组中每一个元素用来承装对应的字符。遍历字符串，用方向控制变量控制按之字形装入stringbuilder数组，最后合并数组。
# java代码
```java
public class Solution {
    public String convert(String s, int nRows) {
         if(s == null || s.equals("")){
            return "";
        }
         if(nRows == 1){
            return  s;
        }
        char[] arr = s.toCharArray();
        StringBuilder res = new StringBuilder();
        StringBuilder [] sb = new StringBuilder[nRows];
        for(int i = 0; i <sb.length; i++){
            sb[i] = new StringBuilder();
        }
        boolean dir = true;
        int j = 0;
        for(int i = 0; i < arr.length; i++){
            sb[j].append(arr[i]);
            if(dir){
                j++;
            }else{
                j--;
            }
            if(j == -1){
                dir = true;
                j = 1;
            }else if(j == nRows){
                dir = false;
                j = nRows - 2;
            }
        }
        for(StringBuilder ss : sb){
            res.append(ss);
        }
        return res.toString();
    }
}
```

