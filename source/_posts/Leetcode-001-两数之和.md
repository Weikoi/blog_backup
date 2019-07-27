---
title: Leetcode 001 两数之和
date: 2019-07-26 21:36:41
categories:
- Leetcode
tags:
- Leetcode
- hash
- 面试
---

    给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

    你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

    示例:

    给定 nums = [2, 7, 11, 15], target = 9

    因为 nums[0] + nums[1] = 2 + 7 = 9
    所以返回 [0, 1]

    来源：力扣（LeetCode）
    链接：https://leetcode-cn.com/problems/two-sum
    著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



#### 思路主要就是用一个hash去做存储，空间换时间的典型思路。


1. Java写法：
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> hs = new HashMap<>();
        for(int i=0; i<nums.length;i++){
            if(hs.containsKey(target - nums[i])) return new int[]{i, hs.get(target - nums[i])};
            else hs.put(nums[i], i);
        }
        return null;
    }
}
```

2. Python写法：
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        
        demo_dict = {}
        for idx,i in enumerate(nums):
            if (target-i) in demo_dict.keys():
                return [idx, demo_dict[target-i]]
            else:
                demo_dict[i] = idx
        return None
        
```