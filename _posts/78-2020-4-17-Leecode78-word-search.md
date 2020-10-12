---
layout:     post
title: Leecode
subtitle:    Leecode78-word-search
date:       2020-04-17
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - Leecode
---


# 题目描述
给出一个二维字符数组和一个单词，判断单词是否在数组中出现，
单词由相邻单元格的字母连接而成，相邻单元指的是上下左右相邻。同一单元格的字母不能多次使用。
例如：
给出的字符数组=
[↵  ["ABCE"],↵  ["SFCS"],↵  ["ADEE"]↵]
单词 ="ABCCED", -> 返回 true,
单词 ="SEE", ->返回 true,
单词 ="ABCB", -> 返回 false.
# java 代码
```java
public class Solution {
    public boolean exist(char[][] board, String word) {
       if(board == null){return false;}
        boolean used [][] = new boolean [board.length][board[0].length];
        char [] words = word.toCharArray();
        for(int i =0;i < board.length;i++){
            for(int j =0; j < board[0].length;j++){
                if(existHelp(board,used,i,j,words,0)){
                    return true;
                }
            }
        }
        return false;
        
    }
    //给一二维字符集 以及访问记录 问从 x y 处 能否找到 words index之后的字符 （包含index）
    public boolean existHelp(char [][] board,boolean [][] used,int x,int y,char [] words,int index){
        //如果index 超出了words下标 说明已经搜索完了全部
        if(index == words.length){return true;}
        /*如果能返回true 必须是
            1.该坐标没有越界
            2.该坐标的字符和words[idnex]一致，而且之前没有使用过 
            3.相邻的四个方向之一，可以找到index之后的字符
           */
       if(x >= board.length || x <0 || y >= board[0].length || y<0 || used[x][y] || board[x][y] != words[index]){return false;}
        
        used[x][y] = true;
        //四个方向 任意一个为起点 可以找到index之后的串，能够连续  都可以
        if(existHelp(board,used,x-1,y,words,index+1)){
            return true;
        }
        if(existHelp(board,used,x+1,y,words,index+1)){
            return true;
        }
        if(existHelp(board,used,x,y-1,words,index+1)){
            return true;
        }
        if(existHelp(board,used,x,y+1,words,index+1)){
            return true;
        }       
        used[x][y] = false;
       //四个方向都不行 表示从x y 找不到
        return false;
    }
}
```