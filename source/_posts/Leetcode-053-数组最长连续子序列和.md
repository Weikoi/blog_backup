---
title: Leetcode 053 数组最长连续子序列和
date: 2019-09-05 20:58:10
categories:
- Leetcode
tags:
- Leetcode
- DP
- 面试
---

---

    给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

    示例:

    输入: [-2,1,-3,4,-1,2,1,-5,4],
    输出: 6
    解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。

    进阶:

    如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。

    来源：力扣（LeetCode）
    链接：https://leetcode-cn.com/problems/maximum-subarray
    著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


#### 动态规划问题，判断的状态只有一个，那就是当前的最长连续子序列和，那么这个状态会有几种可能得到？答案是两种，其一是前一状态加上当前数字。其二就是当前数字。


1. Java写法：
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int res = nums[0];
        
        int[] dp = nums;
        
        for(int i=1; i<nums.length; i++){
            
            dp[i] = Math.max(dp[i-1]+dp[i], dp[i]);
            
            if(dp[i]>res){
                res=dp[i];
            }
        }
        return res;
        
    }
}
```

2. Python写法：
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        dp = nums
        res = nums[0]
        for i in range(1, len(nums)):
            dp[i] = max(dp[i]+dp[i-1], dp[i])
            res = max(res, dp[i])
        return res
```   
