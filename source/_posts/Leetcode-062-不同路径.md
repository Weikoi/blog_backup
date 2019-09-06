---
title: Leetcode 062 不同路径
date: 2019-09-05 21:51:08
categories:
- Leetcode
tags:
- Leetcode
- DP
- 面试
---

---
    一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

    机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

    问总共有多少条不同的路径？


    说明：m 和 n 的值均不超过 100。

    示例 1:

    输入: m = 3, n = 2
    输出: 3
    解释:
    从左上角开始，总共有 3 条路径可以到达右下角。
    1. 向右 -> 向右 -> 向下
    2. 向右 -> 向下 -> 向右
    3. 向下 -> 向右 -> 向右

    示例 2:

    输入: m = 7, n = 3
    输出: 28

    来源：力扣（LeetCode）
    链接：https://leetcode-cn.com/problems/unique-paths
    著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


#### 动态规划问题，每一格的路径数都是等于它左边和上边格子的路径数目之和，其中要注意的是，第一行和第一列都只有一种路径。


1. Java写法：
```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
        
        for(int i=0;i<m;i++){
            dp[i][0] = 1;
        }
        
        for(int i=0;i<n;i++){
            dp[0][i] = 1;
        }
        
        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                dp[i][j] = dp[i][j-1] + dp[i-1][j];
            }
        }
        return dp[m-1][n-1];
    }
}
```

2. Python写法：
```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[0 for i in range(n)] for j in range(m)]
        
        for i in range(m):
            dp[i][0] = 1
        
        for i in range(n):
            dp[0][i] = 1
            
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i-1][j] + dp[i][j-1]
        
        return dp[m-1][n-1]
```   

