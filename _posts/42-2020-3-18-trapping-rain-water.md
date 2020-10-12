---
layout:     post
title: Leecode
subtitle:    trapping-rain-water
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
给出n个数字，表示一个高程图，高程图中每一条的宽度为1，请计算下雨之后这个地形可以存储多少水
例如
给出[0,1,0,2,1,0,1,3,2,1,2,1],返回6.
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020031819455114.png)
上面的高程图用数组[0,1,0,2,1,0,1,3,2,1,2,1]表示。在这种情况下，6个单位的雨水（蓝色部分）被存储。

# 分析
* 用 i j 两个指针分别从前向后，从后向前运动。
*  用 leftmax 记录 i 指针遍历过的最大值
* 用 rightmax 记录j 指针遍历过的最大值
* 相当于 i 左边 ，j右边的边界是已知的
* 如果 leftmax  < rightmax 由于短板效应，i 处的水量一定取决于leftmax，无论i j之间有更高的或者更矮的。
* 反之，可以计算j处的水量。
# java 代码
```java
public class Solution {
    public int trap(int[] A) {
        if(A == null || A.length < 3){
            return 0;
        }
        
        int i = 0;
        int j = A.length - 1;
        int leftmax = 0;
        int rightmax = 0;
        int res = 0;
        while(i <= j){
            //记录 i左边最高的（包括i）
            leftmax = Math.max(leftmax,A[i]);
            // j右边最高的（包括j）
            rightmax = Math.max(rightmax,A[j]);
            //此时对于 i j 他们左边和右边的边界（就像是桶的最短边一样）已经知道了
            if(leftmax < rightmax){
                res += leftmax - A[i]; 
                i++;
            }else{
                res += rightmax - A[j]; 
                j--;
            }
        }
        return res;
        
    }
}
```