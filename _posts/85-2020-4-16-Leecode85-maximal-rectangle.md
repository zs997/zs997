---
layout:     post
title: Leecode
subtitle:    Leecode85 maximal-rectangle
date:       2020-04-15
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
给出一个只包含0和1的二维矩阵，找出最大的全部元素都是1的长方形区域，返回该区域的面积
# 分析
* 可以借用 Leecode84 largest-rectangle-in-histogram。
* 按行计算，计算从第0行到第i行，每一列连续的1个数，如果有0就归零。这相当于从第0行到第i行的高度。
* 计算每行可以达到的最大面积。
# 代码实现
```java
import java.util.Stack;
public class Solution {    
     public int maximalRectangle(char[][] matrix) {
        if(matrix == null || matrix.length == 0){
            return 0;
        }
        int height [][] = new int [matrix.length][matrix[0].length];
        for (int i = 0; i < height[0].length; i++) {
            height[0][i] = matrix[0][i] - '0';
        }
        int max = largestRectangleArea(height[0]);
        for (int i = 1; i < matrix.length; i++) {
            //遍历每一行
            for (int j = 0; j < matrix[i].length; j++) {
                if(matrix[i][j] == '0'){
                    height[i][j] = 0;
                }else{
                    // '1'
                    height[i][j] = height[i-1][j] + 1; 
                }
            }
            max = Math.max(max,largestRectangleArea(height[i]));

        }
        return max;
    }
    
     public static int largestRectangleArea(int[] height) {
        if(height == null || height.length == 0){
            return  0;
        }
        //装下标 递增元素下标 push
        Stack<Integer> stack = new Stack<>();
        int max = 0;
        for (int i = 0; i < height.length; i++) {
            //递增 push
            if(stack.empty() || height[i] >= height[stack.peek()]){
                stack.push(i);
            }else{
                //要考虑的高度  计算影响范围
                int h = height[stack.pop()];
                //考虑等高
                while (!stack.empty() && h == height[stack.peek()]){
                    stack.pop();
                }
                //因为stack递增加入的 所以弹出第一个不为h的  就是h的左边界
                int left = stack.empty()?-1:stack.peek();
                //i是右边界 i比 栈顶小
                max = Math.max(max,(i-left-1)*h);
                //下一次还要继续考虑这个i
                i--;
            }
        }
        //stack 剩下的全是递增的 而stack的peek一定是最高那个元素 对应的下标 那么有边界+1
        //其他的更低元素  右边界也是这样
        int right = stack.peek()+1;
        while(!stack.empty()){
            int h = height[stack.pop()];
            int left = stack.empty()?-1:stack.peek();
            max = Math.max(max,(right-left-1)*h);
        }
        return max;
    }  
}
```