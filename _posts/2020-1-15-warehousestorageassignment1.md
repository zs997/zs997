---
layout:     post
title: 基于动态规划的库位分配算法
subtitle:   使用拣货路径长度优化人到货拣货的仓库库位分配
date:       2020-01-15
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Dynamic Program
    - Algorithm
    - Schedule
---
# 使用拣货路径长度优化人到货拣货的仓库库位分配
   各位读者大家好，今天ZS给大家分享使用动态规划算法求解库位分配问题。算法的主要思想来自于论文：Exact route-length formulas and a storage location assignment heuristic for picker-to-parts warehouses。动态规划算法一直以来都是让人很摸不到头脑的算法，小编刚开始写这个程序的时候，真是写到崩溃，但是要始终相信社会主义核心价值观，只要思想不滑坡，就可以捋顺思路！言归正传，上！
# 动态规划算法典型算例

![图1 动态规划求解最短路径](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8yMTU5MTU0OC00MjA3M2U1NWMxNGZjOTg4LnBuZw?x-oss-process=image/format,png)
   动态规划算法的核心思想是通过子问题的最优解求解出原问题的最优解。图1 所示，求从A到D的最短路径，如果已知从A到C1的最短路径Pac1，从A到C2的最短路径Pac2，从A到C3的最短路径Pac3，从A到C4的最短路径Pac4。那么从A到D的最短路径是 				               min{Pac1+C1D,Pac2+C2D,Pac3+C3D,Pac4+C4D}
这样逐步向前推进，就可以算得最短路径。

# 库位分配问题简介
![图2 仓库布局](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8yMTU5MTU0OC01YTI2ZTI5MDRiZWE0MTVlLnBuZw?x-oss-process=image/format,png)
	如图2所示，纵向通道两边是货架，用于存货。前后两个横通道连接各货架。纵向通道货架左右对称，入库出库无差别，认为两者属于同一列。
###  简化处理
*    	按需求频率由大到小将货物分为A,B,C三类。（需求频率：给定订单，需要各类货物的占比）
*     货物数目和库位数目相等。各类货物总数一定。
### 目的
*   每一个库位匹配合理的货物类型
# 概率假设
* 给定拣货订单，拣选每个A的概率都相等，B,C同理。
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8yMTU5MTU0OC0wZjM5MDRiZGJjZTBmNTZhLnBuZw?x-oss-process=image/format,png)
* 每个货物都有一定概率被拣选，将货物分配到库位中，也就确定了在某处拣货的概率。pij是本算法中比较关键的变量。
* 货物在仓库中的分布优化问题 ------>>>> 仓库中的拣货概率分布问题
# 评价指标-平均拣货路径长度

![图3 以返回式拣货策略
为例（共四种）](https://img-blog.csdnimg.cn/20200307125138618.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDMwMDcwMg==,size_16,color_FFFFFF,t_70)


![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8yMTU5MTU0OC0zMjU4ZTg4MmM3YWVlYmU3LnBuZw?x-oss-process=image/format,png)

![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8yMTU5MTU0OC02NzI5NjIzYmRmZTRmMmFhLnBuZw?x-oss-process=image/format,png)

![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8yMTU5MTU0OC01YzFkMzRlNDJmMWJlM2E1LnBuZw?x-oss-process=image/format,png)


![图 4 目标函数](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8yMTU5MTU0OC04Mjc2NWRhNjk1Y2FkMjYyLnBuZw?x-oss-process=image/format,png)
图4以图3中的拣货路径策略为例，求解给定一概率分布下，平均拣货路径长度，以此作为目标函数，优化仓库中货物的类别分布。

#  动态规划求解库位分配问题
以4×4格局仓库，A,B两种货物说明动态规划算法：
用v[m][na][nb]表示子问题，将货物na,nb分配到前m通道。

![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8yMTU5MTU0OC1jZmY2OWZmZTI4NTI1ZjVlLnBuZw?x-oss-process=image/format,png)

![图5 动态规划求解库位分配问题](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8yMTU5MTU0OC03MjA4ZWM4ZWZhNjk1YTkxLnBuZw?x-oss-process=image/format,png)

```c++
/*
		动态规划算法的伪代码
*/
for i←0 to all
      for j←0 to all-i
            k←all-i-j
            if   i,j,k 不符合约束条件 
                 then continue
             culum cu(i,j,k)
            cu.Sofar_length←某较大的数
            for o←0 to all_last
	for p←0 to all_last-o
	      q←all_last-o-p
	      if  o,p,q 不符合约束条件 
	           then continue
  	      计算 zi
	      culum cu(zi)
	     cu.计算转化成本
	     if  转换成本+v[m-1][o][p]<cu.Sofar_length
                            更新 cu
v[m][i][j]←cu
```
# 代码实现
```c++
/************************动态规划算法的核心*************************************************************/
 void calcul::doDP(vector<answer> *ans)
{
	culum ***v;
	v=new culum **[M];	
	for(int m=0;m<M;m++)
	{	
		if(m==0)
		{
			int all=N;
			v[0]=new culum * [all+1];
			for(int i=0;i<=all;i++)
				{
					 v[0][i]=new culum[all-i+1];
					for(int j=0;j<=all-i;j++)		
					{
						int k=all-i-j;
						if(calcul::panduan(i,j,k))//判断是否满足各类数目小于总货物数
							continue;
						culum cu; 

						cu.calcul_cost(1,i,j,k,i,j,k); // 第一批i,j,k到某通道用到的货物个数统计，第二批ijk该通道货物数统计
				
						cu.set_lastABC(0,0,0);

						cu.Sofar_length=cu.get_cost();
						v[m][i][j]=cu;
					}
				}
		}		
		else if(m!=(M-1)) //不是最后一个通道也不是第一个通道的情况 
		{
			int all=N*(m+1);
			v[m]=new culum *[all+1];
			for(int i=0;i<=all;i++)
				{
					v[m][i]=new culum[all-i+1];
					for(int j=0;j<=all-i;j++)		
					{
						int k=all-i-j;
						if(calcul::panduan(i,j,k)) //判断是否满足各类数目小于总货物数
							continue;					
						int all_last=N*m;
						
						culum cu;
						culum cu_temp; 

						cu.Sofar_length=9999;
						//穷举前一个通道所有状态解，就是查询数组，并且和本阶段的状态结合，取最优
						for(int o=0;o<=all_last;o++)//穷举上一个通道解的状态
							{
								for(int p=0;p<=all_last-o;p++)
								{	
									int q=all_last-o-p;
									if(calcul::panduan(o,p,q)) //判断是否满足各类数目小于总货物数
										continue;
									int ma=i-o; 	// (i-o) m通道a个数 
									int mb=j-p;		//(j-p)  m通道b个数
									int mc=k-q;  	//(all-i-j)-(all_last-o-p)  m通道c个数
									if((ma<0)||(mb<0)||(mc<0)) //m通道不可行  但是没有用最优化条件
										continue;	
									if((ma+mb+mc)!=N)  //这一项是必须的 保证ma(或者mb,mc)不超过N
										continue;  //只有加和为N才能继续运行 否则跳转
									int lastI=o-v[m-1][o][p].lastA;
									int lastJ=p-v[m-1][o][p].lastB;
								//	int lastK=q-v[m-1][o][p].lastC;
									if(ma>lastI||(ma+mb)>(lastI+lastJ)) //最优化条件，条件要搞清楚
										continue;	
								
									cu_temp=v[0][ma][mb]; //单个通道的库位分配 只有库位分配 ELi enterprob有价值
								
									cu_temp.calcul_cost(m+1,i,j,k); //计算lastprob,Elc,以及cost 
								
								
									if(v[m-1][o][p].Sofar_length+cu_temp.get_cost()<cu.Sofar_length)
									{
										cu=cu_temp; //除了Sofar_length和 lastABC都已经更新完毕

										cu.Sofar_length=v[m-1][o][p].Sofar_length+cu.get_cost();

										cu.set_lastABC(o,p,q);//cu.lastA=o;cu.lastB=p;cu.lastC=q;									
									//这里m=2~M-2是第3~M-1通道 ，o p 是状态(m,i,j)的上一状态最优解
									}														
								}

							}

						v[m][i][j]=cu;						
					}
				}
		
		}
		else //对应最后一个通道情况 m=M-1时
		{
			int i=overall_A;
			int j=overall_B;
			int k=overall_C;
			v[m]=new culum *[1];
			v[m][0]=new culum[1];

			int all_last=N*m;	
			
			culum cu; //1 代表通道号
			cu.Sofar_length=9999;
			culum cu_temp; 
			//穷举前一个通道所有状态解，就是查询数组，并且和本阶段的状态结合，取最优
			for(int o=0;o<=all_last;o++)//穷举上一个通道解的状态
				{
				for(int p=0;p<=all_last-o;p++)
					{	
						int q=all_last-o-p;
						if(calcul::panduan(o,p,q)) //判断是否满足各类数目小于总货物数
							continue;
						int ma=i-o; 	// (i-o) m通道a个数 
						int mb=j-p;		//(j-p)  m通道b个数
						int mc=k-q;  	//(all-i-j)-(all_last-o-p)  m通道c个数	
						if((ma+mb+mc)!=N)
							continue;
						if(ma<0||mb<0||mc<0) //m通道不可行  但是没有用最优化条件
							continue;				
						int lastI=o-v[m-1][o][p].lastA;
						int lastJ=p-v[m-1][o][p].lastB;
					//	int lastK=q-v[m-1][o][p].lastC;
						if(ma>lastI||(ma+mb)>(lastI+lastJ)) //最优化条件
							continue;					
																
						cu_temp=v[0][ma][mb];

						cu_temp.calcul_cost(m+1,i,j,k);
					
						if(v[m-1][o][p].Sofar_length+cu_temp.get_cost()<cu.Sofar_length)
						{
							cu=cu_temp;
							cu.Sofar_length=v[m-1][o][p].Sofar_length+cu.get_cost();
							cu.set_lastABC(o,p,q);//cu.lastA=o;cu.lastB=p;cu.lastC=q;			
							//这里m=2~M-2是第3~M-1通道 所以 o p 是状态(m,i,j)的第一个通道最优解				
						}	
									
					}
				}
			v[m][0][0]=cu;						
		}
	}
```
#  实验结果
![图6 输入数据示例](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8yMTU5MTU0OC1mNTdlZTlmZDFkMDc5MTNkLnBuZw?x-oss-process=image/format,png)

![图7 输出数据示例](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8yMTU5MTU0OC1mMzIzMDdmMjQzNzAyMjA5LnBuZw?x-oss-process=image/format,png)

在图7 中每一行代表仓库的一条通道。第1列是通道编号，第2、3、4列是各类货物的数目，最后一列是评价值。

#  参考文献

[1]Arjan S. Dijkstra,Kees Jan Roodbergen. Exact route-length formulas and a storage location assignment heuristic for picker-to-parts warehouses[J]. Transportation Research Part E,2017,102.
[2] 源代码地址：https://github.com/zs997/warehouse


