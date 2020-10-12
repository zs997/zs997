---
layout:     post
title: Leecode
subtitle:    Leecode75 sort-colors
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
现在有一个包含n个物体的数组，其中物体颜色为颜色为红色、白色或蓝色，请对这个数组进行排序，让相同颜色的物体相邻，颜色的顺序为红色，白色，蓝色。
我们用0,1,2分别代表颜色红，白，蓝
注意：
本题要求你不能使用排序库函数
扩展：
一个非常直接的解法是两步的计数排序的算法
首先：遍历一遍数组，记录0,1,2的数量，然后重写这个数组，先将0写入，再将1写入，再将2写入
你能给出一个只用一步，并且能在常数级空间复杂度解决这个问题的算法吗？
# 分析
* 通俗讲就是，由0,1,2组成的数组，就地算法进行排序。
* 设置left，right指针，分别left左边全是0，left指向从左边数第一个非0元素，right指向从右边数，第一个非2元素。
* cur左边保证是0后者1。
* cur从left移动到right，碰到1跳过去；碰到2，和right处元素交换，right处的元素是0或者1，此时right被换成了2，right--；碰到0，和left处元素交换，因为cur左边只是0或者1,那么left指向的元素一定是1，做完此交换后，left指向的元素变成了0，left可以右移。此时cur处的元素是1，也要右移。
# java 代码
```java 
public class Solution {
    public void sortColors(int[] A) {
        if(A == null || A.length <= 1){
            return;
        }
        //本质就是0 1 2元素的数组排序
        //left 从左向右 指向第一个非0元素
        int left = 0;
        while(left < A.length && A[left] == 0){
            left++;
        }
        //right 从右向左 指向第一个非2 元素
        int right = A.length-1;
        while(right > 0 && A[right] == 2){
            right--;
        }
        int cur = left;
        
        while(cur <= right){
            if(A[cur] == 1){ 
                cur++;
            }else if(A[cur] == 0){
                swap(A,cur,left);
               left++;
                cur++;
            }else{               
                swap(A,cur,right);
                right--;               
            }
        }
    }    
    public void swap(int [] A, int i ,int j){
        int temp = A[i];
        A[i] = A[j];
        A[j] = temp;
    }
}
```