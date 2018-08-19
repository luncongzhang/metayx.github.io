---
layout: post
title:  "258. 各位相加"
categories: 算法
tags: leetcode 数学
---

* content
{:toc}

<!--more-->

给定一个非负整数 num，反复将各个位上的数字相加，直到结果为一位数。

示例:

```
输入: 38
输出: 2 
解释: 各位相加的过程为：3 + 8 = 11, 1 + 1 = 2。 由于 2 是一位数，所以返回 2。
```

进阶:
* 你可以不使用循环或者递归，且在 O(1) 时间复杂度内解决这个问题吗？

解：神奇代码。

```
class Solution {
    public int addDigits(int num) {
        if (num < 10) {
            return num;
        }
        return num % 9 == 0 ? 9 : num % 9;
    }
}
```