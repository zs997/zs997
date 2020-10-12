---
layout:     post
title: Leecode
subtitle:    Leecode73 set-matrix-zeroes
date:       2020-04-10
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
给定一个m*n的矩阵，如果有一个元素是0，就把该元素所在的行和列上的元素全置为0，要求使用原地算法。
拓展：
你的算法有使用额外的空间吗？
一种比较直接的算法是利用O(m,n)的空间，但是这不是一个好的解法
使用简单的改进可以在O(m+n)的空间解决这个问题，但是还不是最佳的解法
你能在常量级的空间复杂度内解决这个问题吗？
# 分析
* 假设第0行与第0列都没有0，那么第0行和第0列可以标志其他元素所在行列是否要置空。比如 matrix[2][3] = 0,那么可以置 matrix[2][0] = 0,matrix[0][3] = 0,表示第二行和第三列都要置零。
# java 代码
```java
public class Solution {
    public void setZeroes(int[][] matrix) {
        //行数
        int rows = matrix.length;
        //列数
        int cols = matrix[0].length;
        //行标记
        boolean row_flag = false;
       //列标记
        boolean col_flag = false;
        //看第0列是否有0
        for(int i = 0; i < rows;i++){
            if(matrix[i][0] == 0){
                col_flag = true;
                break;
            }
        }
        //看第0行是否有0
        for(int i = 0; i < cols;i++){
            if(matrix[0][i] == 0){
                row_flag = true;
                break;
            }
        }
        //检查除了第0行和第0列之外，是否有0，当然如果第0行，第0列本身就有0不会改变
        for(int i = 1; i < rows; i ++){
            for(int j = 1; j < cols; j++){
                if(matrix[i][j] == 0){
                    //同一行的标记 归零
                    matrix[i][0] = 0;
                    //同一列标记 归零
                    matrix[0][j] = 0;
                }
            }
        }        
        //遍历元素，检查自己是否在归零范围内
        for(int i = 1;i < rows;i++){
            for(int j = 1; j <cols;j++){
                if(matrix[i][0] == 0 ||matrix[0][j] == 0){
                    matrix[i][j] = 0;
                }
            }
        }
        //行标记 将第0行置零
        if(row_flag){
            for(int i = 0; i < cols;i++){
                matrix[0][i] = 0;
            }
        }
        //列标记 将第0列置零
        if(col_flag){
            for(int i = 0; i < rows;i++){
                matrix[i][0] = 0;
            }
        }    
    }    
}
```