---
title: Leetcode 002 两数相加
date: 2019-07-27 13:36:57
categories:
- Leetcode
tags:
- Leetcode
- 链表
- 面试
---

    给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

    如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

    您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

    示例：

    输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
    输出：7 -> 0 -> 8
    原因：342 + 465 = 807

    来源：力扣（LeetCode）
    链接：https://leetcode-cn.com/problems/add-two-numbers
    著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


#### 思路主要就是用一个hash去做存储，空间换时间的典型思路。


1. Java写法：
```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode cur1 = l1;
        ListNode cur2 = l2;
        
        
        ListNode init = new ListNode(0);
        ListNode cur = init;
        
        int temp=0;
        
        while(cur1!=null || cur2!=null){
            
            temp /=10;
            if(cur1!=null){
                temp+=cur1.val;
                cur1=cur1.next;
            }
            if(cur2!=null){
                temp+=cur2.val;
                cur2=cur2.next;
            }
            
            cur.next = new ListNode(temp%10);
            cur = cur.next;
        }
        
        if(temp/10!=0){
            cur.next = new ListNode(1);
        }
        return init.next;
        
    }
}
```

2. Python写法：
```python
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        
        # 移动指针
        cur1 = l1
        cur2 = l2
        
        init = ListNode(0)
        cur = init
        
        temp=0
        
        while cur1 or cur2:
            temp //=10
            
            if cur1:
                temp+=cur1.val
                cur1=cur1.next
            if cur2:
                temp+=cur2.val
                cur2=cur2.next
            
            cur.next = ListNode(temp%10)
            cur = cur.next
        
        if temp//10!=0:
            cur.next = ListNode(1)
        
        return init.next
        
```