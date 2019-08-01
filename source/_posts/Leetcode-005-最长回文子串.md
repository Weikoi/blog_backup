---
title: Leetcode 005 最长回文子串
date: 2019-07-30 21:53:42
categories:
- Leetcode
tags:
- Leetcode
- DP
- 面试
---
---

    给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

    示例 1：

    输入: "babad"
    输出: "bab"
    注意: "aba" 也是一个有效答案。

    示例 2：

    输入: "cbbd"
    输出: "bb"

    来源：力扣（LeetCode）
    链接：https://leetcode-cn.com/problems/longest-palindromic-substring
    著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


#### 动态规划问题，分为两种一般情况，若子串长度为2，那么是否回文只取决于两个字符是否相等；若长于2，取决于比他短的子串是否回文且末端字符是否相等。


1. Java写法：
```java
class Solution {
    public String longestPalindrome(String s) {
        int length = s.length();
        if(length==0 || length==1) return s;

        int start=0;
        int end=0;

        Boolean[][] dp = new boolean[length][length];

        for(int i=0;i<length;i++){
            dp[i][i] = true;
            for(int j=0;j<i;j++){
                if(j+1==i) return s.charAt(j)==s.charAt(i);
                else return (s.charAt(j)==s.charAt(i))&&(dp[j+1][i-1]);

                if(i=j>end-start){
                    end=i;
                    start=j;
                }
            }
        }
        return s.substring(start, end+1);
    }
}
```

2. Python写法：
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        length = len(s)
        dp = [[False for i in range(length)] for i in range(length)]
        start = 0
        end = 0

        for idx1 in range(length):
            dp[idx1][idx1] = True
            for idx2 in range(idx1):
                if idx2 + 1 == idx1:
                    dp[idx2][idx1] = (s[idx1] == s[idx2])
                else:
                    dp[idx2][idx1] = (s[idx1] == s[idx2]) and (dp[idx2 + 1][idx1 - 1])
                if (dp[idx2][idx1]) and (end - start < idx1 - idx2):
                    end = idx1
                    start = idx2
                    print(idx2, idx1)
        return s[start:end+1]
```   
