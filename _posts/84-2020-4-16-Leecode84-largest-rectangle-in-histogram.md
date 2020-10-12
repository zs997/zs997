---
layout:     post
title: Leecode
subtitle:    Leecode84 largest-rectangle-in-histogram
date:       2020-04-16
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
给出n个数字，代表直方图的条高，直方图每一条的宽度为1，请计算直方图中最大矩形的面积
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200415212627261.png)
上图是每条宽度为1, 高度 =[2,1,5,6,2,3].的直方图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200415212643143.png)
图中的阴影部分是该直方图中面积最大的矩形，面积为10个单位
例如：
给出的高度 =[2,1,5,6,2,3],
返回10.
# 分析
* 使用栈结构，数组存储下标，元素递增压栈。
* 遇到不是递增的情况，说明栈顶元素的右边界出现了。
* 此时弹出栈顶，计算它能横向覆盖多长。
* 此时栈顶是左边界。
* 计算面积，更新最大值。
* 之后，栈顶的剩余只有递增的元素，采用相同的方法。
# 代码
```java
import java.util.Stack;
public class Solution {
    public int largestRectangleArea(int[] height) {
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