---
layout:     post
title: Leecode
subtitle:    Leecode72 edit-distance
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
给定两个单词word1和word2，请计算将word1转换为word2至少需要多少步操作。
你可以对一个单词执行以下3种操作：
a）在单词中插入一个字符
b）删除单词中的一个字符
c）替换单词中的一个字符
# 分析
* 使用动态规划算法。
	* 状态表示 ：dp [i][j]：word1前i个字符子串变成word2前j个字符子串需要的步数。
	* 初始化：一方为空，变成另一方，只需要插入所有另一方的字符，操作次数和另一方长度一致。
    * 状态递推：
    			* 如果word1[i] ==word2[j]：dp[i][j] = min{ 1、dp[i-1][j]+1,2、dp[i][j-1]+1,3、dp[i-1][j-1]}，1：表示如果word1少一个字符变成了word2，则步数加1，因为要删除那个字符。2：表示如果word1变成少一个字符的word2，则需要加1步，增加缺失的字符。3：表示如果word1少一个字符变成word2少一个字符，那么步数相等。
    			* 如果word1[i] ！=word2[j]：dp[i][j] = min{ 1、dp[i-1][j]+1,2、dp[i][j-1]+1,3、dp[i-1][j-1]}，1：表示如果word1少一个字符变成了word2，则步数加1，因为要删除那个字符。2：表示如果word1变成少一个字符的word2，则需要加1步，增加缺失的字符。3：表示如果word1少一个字符变成word2少一个字符，那么还需要替换最后一个字符，步数加1。
# java 代码
```java
public class Solution {
    public int minDistance(String word1, String word2) {
        if(word1==null ||word2 == null ){
            return 0;
        }
        if(word1.length() == 0){
            return word2.length();
        }        
        if(word2.length() == 0){
            return word1.length();
        }
        int m = word1.length();
        int n = word2.length();
        //word1 前i个字符子串 变成word2 前j个字符子串需要的步数。
        //0 1 2 3 **** m 多一个 
        int dp [][] = new int [m+1][n+1];
        //初始化
        for(int i = 0; i <= m; i++){
            //不同的word1 变成word2（空） 需要的步数 删去长度个字符
            dp[i][0] = i;            
        }
        for(int i = 0; i <= n; i++){
            //word1 为空 变成word2（不同的） 需要添加长度个字符
            dp[0][i] = i;
        }        
        for(int i = 1;i <= m;i++){
            for(int j = 1;j <= n;j++){
                //先给最大值 以防出问题
                //word1 前i个字符 word2 前j个字符
                dp[i][j] = Integer.MAX_VALUE;
                //第i个字符时i-1下标
                if(word1.charAt(i-1) == word2.charAt(j-1)){
                    dp[i][j] = Math.min(dp[i][j],dp[i-1][j]+1);
                    dp[i][j] = Math.min(dp[i][j],dp[i][j-1]+1);
                    dp[i][j] = Math.min(dp[i][j],dp[i-1][j-1]);
                }else{                   
                    dp[i][j] = Math.min(dp[i][j],dp[i-1][j]+1);
                    dp[i][j] = Math.min(dp[i][j],dp[i][j-1]+1);
                    dp[i][j] = Math.min(dp[i][j],dp[i-1][j-1]+1); 
                }
            }
        }
        return dp[m][n];
    }
}
```