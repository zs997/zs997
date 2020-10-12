---
layout:     post
title: Leecode
subtitle:     count-and-say
date:       2020-03-18
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---

# 题目描述
count-and-say数列的前几项如下：

1, 11, 21, 1211, 111221, ...
1读作“1个1”或11
11读作“2个1“或者21
21读作”1个2，1个1“或者1211
给出一个整数n，请给出序列的第n项
注意：序列中的数字用字符串表示
# 分析
* 从上一个数字，到下一个数字，建立一种计算关系。
* 从1开始计算，计算 n-1 次，得到第n个数字。
*  使用 pre 记录上一位数字，使用 count 计算上一位数字出现次数。
* 遇到不同于pre的位，将 count + pre 记录Stringbuffer上。
* 遍历完之后，产生下一位的字符串。
# java 代码
```java 
public class Solution {
    public String countAndSay(int n) {
        if(n <= 0){
            return "";
        }        
        String  str = "1";        
        for(int i = 1; i < n; i++){
            
            int count = 0;
            char pre = '*';
             StringBuffer sb = new StringBuffer(); 
            for(int j = 0; j < str.length(); j++){
                if(str.charAt(j) == pre || pre == '*'){
                    count ++;
                }else{
                    sb.append(count+Character.toString(pre));
                    count = 1;
                }
               pre =  str.charAt(j);
            }
            sb.append(count+Character.toString(pre));
            str = sb.toString();
        }
        return str;
    }
}

```