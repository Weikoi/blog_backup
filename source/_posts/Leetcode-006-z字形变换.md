---
title: Leetcode 006 z字形变换
date: 2019-12-09 16:46:41
categories:
- Leetcode
tags:
- Leetcode
- 面试
---
---

    将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。

    比如输入字符串为 "LEETCODEISHIRING" 行数为 3 时，排列如下：

    L   C   I   R
    E T O E S I I G
    E   D   H   N

    之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："LCIRETOESIIGEDHN"。

    请你实现这个将字符串进行指定行数变换的函数：

    string convert(string s, int numRows);

    示例 1:

    输入: s = "LEETCODEISHIRING", numRows = 3
    输出: "LCIRETOESIIGEDHN"

    示例 2:

    输入: s = "LEETCODEISHIRING", numRows = 4
    输出: "LDREOEIIECIHNTSG"
    解释:

    L     D     R
    E   O E   I I
    E C   I H   N
    T     S     G

    来源：力扣（LeetCode）
    链接：https://leetcode-cn.com/problems/zigzag-conversion
    著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


#### 有限状态机FSM思想，状态只有两种，向上和向下和所处的行数，注意状态间的切换。


1. Java写法：
```java
class Solution {
    public String convert(String s, int numRows) {
        
        if (numRows == 1) return s;

        List<StringBuilder> str_list = new ArrayList<>();
        for (int i = 0; i < Math.min(numRows, s.length()); i++)
            str_list.add(new StringBuilder());

        int curRow = 0;
        int goingDown = 1;

        for (char c : s.toCharArray()) {
            str_list.get(curRow).append(c);
            if ((goingDown ==-1 && curRow == 0) || (goingDown ==1 && curRow == numRows - 1)) goingDown = -1*goingDown;
            if(goingDown==1){
                curRow++;}
            else{curRow--;}
                
        }

        StringBuilder return_str = new StringBuilder();
        for (StringBuilder row : str_list) return_str.append(row);
        return return_str.toString();
        
    }
}
```

2. Python写法：
```python
class Solution {
    public String convert(String s, int numRows) {

        if numRows<2:
            return s
        
        # 存储结构初始化
        total_list = [[] for i in range(min(numRows, len(s)))]

        # 状态指向，初始为向下
        down = 1
        row = 0

        for i in s；
            total_list[row].append(i)

            # 换方向的两个条件
            if (row==numRows and down==1) or (row==0 and down==-1):
                down*-1

            # 根据方向调整row
            if(down==1):
                row+=1
            elif(down==-1):
                row-=1
        
        return_str = ""
        for each in total_list:
            return_str += "".join(each)
        
        return return_str


        
    }
}
```   

