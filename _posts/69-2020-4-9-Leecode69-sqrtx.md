---
layout:     post
title: Leecode
subtitle:    Leecode69 sqrtx
date:       2020-04-09
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---



# 题目描述
实现函数 int sqrt(int x). 
计算并返回x的平方根

# 分析
* 可以通过数列的概念，将平方和归纳到一种数列。
* 找到数列中，第一个大于x的数，下标就可以求出结果。
# java 代码
```java
public class Solution {
    public int sqrt(int x) {
        if(x <= 0){
            return 0;
        }
        //使用累加法 1 4 9 16 25 ****        
        //这些数的间隔是 3 5 7 9 ***
        //间隔自增2     
        int res = 0;
        int delta = 1;
        int index = 0;
        //找出第一个大于x的res和index
       while(res <= x){
           //如果x比较大 接近于 Integer.MAX_VALUE。
           //sqrt（Integer.MAX_VALUE）^2 可能比Integer.MAX_VALUE小很多
           //如果继续增量delta，会出现错误，而事实上，这些数x的解就已经算出来了
           if(Integer.MAX_VALUE - res < delta){
               return index ;
           }
            res += delta;
            delta += 2;
            index ++;
        }
        //出来循环的 一定是大于x的res
        return index - 1;
    }
}
```