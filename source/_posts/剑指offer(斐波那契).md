---
title: 剑指offer(斐波那契数列)
date: 2020-02-17 10:43:20
tags:
copyright: true
---
* 避免递归造成的调用栈消耗
```
public class Solution {
    public int Fibonacci(int n) {
        int a = 0;
        int b = 1;
        while(n-->0){
            b = a + b;
            a = b - a;
        }
        return a;
    }
}
```
* 复杂度
时间复杂度：O(n)O(n)
空间复杂度：O(1)O(1)
