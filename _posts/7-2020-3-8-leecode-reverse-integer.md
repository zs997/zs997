---
layout:     post
title:  Leecode
subtitle:   reverse-intege
date:       2020-03-8
author:     ZS
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags: 
    - Java
    - Algorithm
    - leecode
---
# 题目描述
将给出的整数x翻转。
例1:x=123，返回321
例2:x=-123，返回-321

你有思考过下面的这些问题么？
如果整数的最后一位是0，那么输出应该是什么？比如10,100
你注意到翻转后的整数可能溢出吗？假设输入是32位整数，则将翻转10000000003就会溢出，你该怎么处理这样的样例？抛出异常？这样做很好，但是如果不允许抛出异常呢？这样的话你必须重新设计函数（比如添加一个额外的参数）。

# 分析
* 实现翻转，从低位依次拿出一位数，每次乘10累加。
* 正负号问题，从数学上讲，负数的操作和正数一样。
* 溢出问题，每次产生翻转数时，检查能否可逆操作。
# java代码
```java
class Solution {
public:
    int reverse(int x) {        
        int res = 0;
        int res_last= 0;
        int wei = 0;
        while(x != 0){            
            wei = x%10;            
            x = x / 10;
            res_last = res;
            res = res * 10 + wei;
            if((res-wei)/10 != res_last){
                return 0;
            }
        }        
        return res;
    }
};
```

