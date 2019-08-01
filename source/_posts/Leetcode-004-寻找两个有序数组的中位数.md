---
title: Leetcode 004 寻找两个有序数组的中位数
date: 2019-07-29 19:55:38
categories:
- Leetcode
tags:
- Leetcode
- recursion
- 面试
- Hard Problem
---

    给定两个大小为 m 和 n 的有序数组 nums1 和 nums2。

    请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。

    你可以假设 nums1 和 nums2 不会同时为空。

    示例 1:

    nums1 = [1, 3]
    nums2 = [2]

    则中位数是 2.0

    示例 2:

    nums1 = [1, 2]
    nums2 = [3, 4]

    则中位数是 (2 + 3)/2 = 2.5

    来源：力扣（LeetCode）
    链接：https://leetcode-cn.com/problems/median-of-two-sorted-arrays
    著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


#### 分解成两个问题，首先是在两个有序数组中找到第N大的数的问题， 然后再根据不同的case求得中位数。


1. Java写法：
```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int len1 = nums1.length;
        int len2 = nums2.length;

        if(len1==0){
            if(len2%2!=0){
                return 1.0*nums2[len2/2];
            }
            return (nums2[len2/2]+nums2[len2/2-1])/2.0
        }
        if(len2==0){
            if(len1%2!=0){
                return 1.0*nums1[len1/2];
            }
            return (nums1[len1/2]+nums1[len1/2-1])/2.0
        }

        int mergeLength = len1 +len2;

        if(mergeLength%2!=0){
            return findKth(nums1, 0, nums2, 0, mergeLength/2 + 1);
        }else{
            return (findKth(nums1, 0, nums2, 0, mergeLength/2)+findKth(nums1, 0, nums2, 0, mergeLength/2 + 1))/2;
        }

    }

    //寻找有序数组 nums1 和 nums2 中，第n大的数字
    double find_kth(int[] a, int a_begin, int[] b, int b_begin, int k) {
           //当a 或 b 超过数组长度，则第k个数为另外一个数组第k个数
        if (a_begin >= a.length)
            return b[b_begin + k - 1];
        if (b_begin >= b.length)
            return a[a_begin + k - 1];
        //k为1时，两数组最小的那个为第一个数
        if (k == 1)
            return Math.min(a[a_begin], b[b_begin]);

        int mid_a = Integer.MAX_VALUE;
        int mid_b = Integer.MAX_VALUE;
        //mid_a / mid_b 分别表示 a数组、b数组中第 k / 2 个数
        if (a_begin + k / 2 - 1 < a.length)
            mid_a = a[a_begin + k / 2 - 1];
        if (b_begin + k / 2 - 1 < b.length)
            mid_b = b[b_begin + k / 2 - 1];
        //如果a数组的第 k / 2 个数小于b数组的第 k / 2 个数，表示总的第 k 个数位于 a的第k / 2个数的后半段，或者是b的第 k / 2个数的前半段
        //由于范围缩小了 k / 2 个数，此时总的第 k 个数实际上等于新的范围内的第 k - k / 2个数，依次递归
        if (mid_a < mid_b)
            return find_kth(a, a_begin + k / 2, b, b_begin, k - k / 2);
        //否则相反
        return find_kth(a, a_begin, b, b_begin + k / 2, k - k / 2);
    }
}
```

2. Python写法：
```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        len1 = len(nums1)
        len2 = len(nums2)

        if(len1==0):
            if(len2%2!=0):
                return 1.0*nums2[len2//2];
            return (nums2[len2//2]+nums2[len2//2-1])/2.0
        if(len2==0):
            if(len1%2!=0):
                return 1.0*nums1[len1//2];
            return (nums1[len1//2]+nums1[len1//2-1])/2.0

        mergeLength = len1 +len2;

        if(mergeLength%2!=0):
            return self.find_kth(nums1, 0, nums2, 0, mergeLength//2+1)
        else:
            return (self.find_kth(nums1, 0, nums2, 0, mergeLength//2)+self.find_kth(nums1, 0, nums2, 0, mergeLength//2 + 1))/2
    
    def find_kth(self, nums1, a_begin, nums2, b_begin, k):
       
        if (a_begin >= len(nums1)):
            return nums2[b_begin + k - 1]
        if (b_begin >= len(nums2)):
            return nums1[a_begin + k - 1]
        
        if (k == 1):
            return min(nums1[a_begin], nums2[b_begin]);
        
        mid_a = 2147483647
        mid_b = 2147483647
        
        if (a_begin + k // 2 - 1 < len(nums1)):
            mid_a = nums1[a_begin + k // 2 - 1];
        if (b_begin + k // 2 - 1 < len(nums2)):
            mid_b = nums2[b_begin + k // 2 - 1];
        
        if mid_a < mid_b:
            return self.find_kth(nums1, a_begin + k // 2, nums2, b_begin, k - k // 2)
        
        return self.find_kth(nums1, a_begin, nums2, b_begin + k // 2, k - k // 2)
```   
