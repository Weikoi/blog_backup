---
title: Leetcode 063 不同路径二
date: 2019-09-05 22:13:07
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

    现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

    网格中的障碍物和空位置分别用 1 和 0 来表示。

    说明：m 和 n 的值均不超过 100。

    示例 1:

    输入:
    [
    [0,0,0],
    [0,1,0],
    [0,0,0]
    ]
    输出: 2
    解释:
    3x3 网格的正中间有一个障碍物。
    从左上角到右下角一共有 2 条不同的路径：
    1. 向右 -> 向右 -> 向下 -> 向下
    2. 向下 -> 向下 -> 向右 -> 向右

    来源：力扣（LeetCode）
    链接：https://leetcode-cn.com/problems/unique-paths-ii
    著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


#### 动态规划问题，每一格的路径数都是等于它左边和上边格子的路径数目之和，其中要注意的是初始化问题，第一行和第一列都只有一种路径，但是在遍历过程中如果有障碍物，那么从这个格子开始剩下的都是0，网格中出现障碍物，那么这个格子的路径也要被置为0。


1. Java写法：
```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int[][] dp = new int[m][n];
        
        for(int i=0; i<m; i++){
            if(obstacleGrid[i][0]==1){
                break;
            }
            dp[i][0]=1;
        }
        for(int i=0; i<n; i++){
            if(obstacleGrid[0][i]==1){
                break;
            }
            dp[0][i]=1;
        }
        
        for(int i=1; i<m; i++){
            for(int j=1; j<n; j++){
                if(obstacleGrid[i][j]==1){
                    dp[i][j]=0;
                }else{
                    dp[i][j] = dp[i-1][j] + dp[i][j-1];
                }
                
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
        if not obstacleGrid:
            return 0

        n = len(obstacleGrid)
        m = len(obstacleGrid[0])

        dp = [[0 for i in range(m)] for i in range(n)]

        for i in range(m):
            if obstacleGrid[0][i] == 1:
                break
            dp[0][i] = 1
            
        for i in range(n):
            if obstacleGrid[i][0] == 1:
                break
            dp[i][0] = 1

        for i in range(1, n):
            for j in range(1, m):
                if obstacleGrid[i][j] == 1:
                    dp[i][j] = 0
                else:
                    dp[i][j] = dp[i - 1][j] + dp[i][j - 1]

        return dp[n - 1][m - 1]
```   

