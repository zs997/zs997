---
layout:     post
title: Leecode
subtitle:    valid-sudoku
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
根据数独的规则Sudoku Puzzles - The Rules.判断给出的局面是不是一个符合规则的数独局面
数独盘面可以被部分填写，空的位置用字符'.'.表示
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318160830721.png)
这是一个部分填写的符合规则的数独局面
# 分析
* 先检查每一行是否有重复的数字。
* 再检查每列。
* 最后检查每一个3*3矩阵。
# java 代码
```java
public class Solution {
    public boolean isValidSudoku(char[][] board) {
        if(board == null || board.length != 9 || board[0].length != 9){return false;}        
        //判断所有行
        for(int row = 0; row < 9; row ++){
            //对于某一行 要有一个判断用的数组
            boolean visited [] = new boolean[9];
            for(int i = 0;i < 9;i++){
                if(board[row][i] != '.'){
                    int temp = board[row][i] - '1';
                    if(visited[temp] == false){
                        visited[temp] = true;
                    }else{
                        return false;
                    }
                }
            }
        }        
         //判断所有列
        for(int col = 0; col < 9; col ++){
            //对于某一列 要有一个判断用的数组
            boolean visited [] = new boolean[9];
            for(int i = 0;i < 9;i++){
                if(board[i][col] != '.'){
                    int temp = board[i][col] - '1';
                    if(visited[temp] == false){
                        visited[temp] = true;
                    }else{
                        return false;
                    }
                }
            }
        }        
        //判断矩阵
        int range [] = {0,3,6};
        for(int rowOff :range){
             for(int colOff :range){
                 boolean visited [] = new boolean[9];
                for(int i = 0; i < 3; i++){
                    for(int j = 0; j < 3; j++){
                        if(board[rowOff + i][colOff + j] != '.'){                            
                            int temp = board[rowOff + i][colOff + j] - '1';
                            if(visited[temp] == false){
                                visited[temp] = true;
                            }else{
                                return false;
                            }
                        }                        
                    }
                }
            }
        }        
        return true;        
    }
}
```