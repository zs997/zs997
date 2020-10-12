---
layout:     post
title: Leecode
subtitle:    xxx
date:       2020-xx-xx
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---
# 题目描述
给出一个用二维矩阵表示的图像
返回该图像顺时针旋转90度的结果
扩展：
你能使用原地算法解决这个问题么？
# 分析
* 按圈旋转，从最外圈到最内圈，进行旋转操作。

![图1 矩阵元素位置交换示意](https://img-blog.csdnimg.cn/20200407161058100.png)

![图 2 红色表示其他元素的移动情况](https://img-blog.csdnimg.cn/20200407161342740.png)
* 每圈都要进行若干次元素交换。
* 每圈交换之后，缩小到新的矩阵，再进行交换。
# java代码
```java
public class Solution {
    public void rotate(int[][] matrix) {        
        int n = matrix.length;        
        int top = 0;
        int bot = n-1;        
        int left = 0;        
        int right = n-1;
        while(n > 1){
            for(int i = 0; i < n-1; i++){
                int temp = matrix[top][left + i];
                matrix[top][left + i] = matrix[bot - i][left];
                 matrix[bot - i][left] = matrix[bot][right - i];
                 matrix[bot][right - i] = matrix[top + i][right];
                matrix[top + i][right] = temp;
               }
            top ++ ;
            bot --;
            left++;
            right--;
            n -= 2;            
        }       
        
    }
}
```