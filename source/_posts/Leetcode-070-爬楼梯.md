---
title: Leetcode 070 爬楼梯
date: 2019-09-06 15:53:42
categories:
- Leetcode
tags:
- Leetcode
- DP
- 面试
---

---
    假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

    每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

    注意：给定 n 是一个正整数。

    示例 1：

    输入： 2
    输出： 2
    解释： 有两种方法可以爬到楼顶。
    1.  1 阶 + 1 阶
    2.  2 阶

    示例 2：

    输入： 3
    输出： 3
    解释： 有三种方法可以爬到楼顶。
    1.  1 阶 + 1 阶 + 1 阶
    2.  1 阶 + 2 阶
    3.  2 阶 + 1 阶

    来源：力扣（LeetCode）
    链接：https://leetcode-cn.com/problems/climbing-stairs
    著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


#### 动态规划问题，每一阶楼梯可能是由前一阶楼梯或者前前一阶楼梯爬过来的，因此总数等于它们的情况之和。


1. Java写法：
```java
class Solution {
    public int climbStairs(int n) {
        int[] dp = new int[n+1];
        
        int res = 0;
        dp[0] = 1;
        dp[1] = 1;
        
        for(int i=2; i<n+1; i++){
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }
}
```

2. Python写法：
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        dp = [1 for i in range(n+1)]
        
        for i in range(2, n+1):
            dp[i] = dp[i-1] + dp[i-2]
        
        return dp[n]
```   
