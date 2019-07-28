---
title: Leetcode 003 无重复字符的最长子串
date: 2019-07-28 12:36:02
categories:
- Leetcode
tags:
- Leetcode
- 滑动窗口
- 面试
---

    给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

    示例 1:

    输入: "abcabcbb"
    输出: 3 
    解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。

    示例 2:

    输入: "bbbbb"
    输出: 1
    解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。

    示例 3:

    输入: "pwwkew"
    输出: 3
    解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
        请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。

    来源：力扣（LeetCode）
    链接：https://leetcode-cn.com/problems/longest-substring-without-repeating-characters
    著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


#### 滑动窗口思想，也可以算是DP的入门级别题目, 唯一的状态是子串的长度，压缩存储为单变量记录。


1. Java写法：
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        
        int length = s.length();
        
        Set<Character> set = new HashSet<>();
        
        int r=0;
        int l=0;
        
        int res=0;
        
        while(r<length && l<length){
            
            if (set.contains(s.charAt(r))){
                set.remove(s.charAt(l));
                r++;
            }else{
                set.add(s.charAt(r));
                r++;
            }
            if(res<r-l) res = r-l;
        }
        return res;
    }
}
```

2. Python写法：
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        l=r=0
        length=len(s)
        res = 0
        
        demo_set = set()
        while l<length and r<length:
            if s[r] in demo_set:
                demo_set.remove(s[l])
                l+=1
            else:
                demo_set.add(s[r])
                r+=1
            if r-l>res:
                res=r-l
        return res
```   