---
layout:     post
title: Leecode
subtitle:    sudoku-solver
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
请编写一个程序，给数独中的剩余的空格填写上数字
空格用字符'.'表示
假设给定的数独只有唯一的解法

这盘数独的解法是：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020031815081639.png)
红色表示填上的解
![在这里插入图片描述](https://img-blog.csdnimg.cn/202003181508316.png)
# 分析
* 这个问题抽象，对于一个9*9矩阵，给它的空白处，依次填入适当的数字。
* 这样就可以归纳出一个穷举问题，每一个空格都有1~9 候选值。需要做的是：
	*	如何依次找到空格。
	*	对空格处的值进行合理性判断。
	*	递归到下一个空格。
	*	在某一层，所有的取值都失败了，要有返回上一层的机制，使上一层继续尝试下一个数字。（回溯）。
	*	找到合理解时，要有正确的返回条件。  
# java 代码
```java
public class Solution {
    public void solveSudoku(char[][] board) {
        if(board == null || board.length != 9 || board[0].length != 9){return;}
        boolean res = SudokuHelper(board,0,0);       
    }
    //给 board【row】【col】填数
    public boolean SudokuHelper(char [][] board, int row,int col){
        
        while(row < 9 && col < 9){
            if(board[row][col] == '.'){break;}
            if(col == 8){
                col = 0;
                row ++;                
            }else{              
                col ++;
            }
        }
        //没有可填充的了 全部完成
        if(row >= 9){
            return true;
        }
        
        //找出下一个填充点
        int rowNew = row + col/8;
        int colNew = (col + 1)%9;    
        
        //所以接下来尝试给 row col 填充数字
        for(int i = 1; i <= 9; i++){
            //检查i的可行性
            if(isValid(board,row,col,i)){
               board[row][col] = (char)(i + '0');
               boolean res = SudokuHelper(board,rowNew,colNew);
               if(res){
                   //填充成功
                   return true;
               }else{
                   //填充失败
                   board[row][col] = '.';
               }               
            }
        }        
        return false;
    }    
    public boolean isValid(char [][] board, int row,int col,int num){        
        for(int i = 0; i < board.length; i++){
            if(board[row][i] == num+'0' || board[i][col] == num + '0'){
                return false;
            }
        }        
        int rowOff = row/3*3;
        int colOff = col/3*3;        
        for(int i = 0;i < 3;i++){
            for(int j = 0; j < 3;j++){
                if(board[rowOff + i][colOff + j] == num + '0'){
                    return false;
                }
            }
        }        
        return true;
    }
}
```