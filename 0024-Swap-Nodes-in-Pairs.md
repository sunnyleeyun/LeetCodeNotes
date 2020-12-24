# 24. Swap Nodes in Pairs


## 題目描述

Given a linked list, swap every two adjacent nodes and return its head.

You may not modify the values in the list's nodes. Only nodes itself may be changed.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg)


**Example 2:**

```
Input: head = []
Output: []
```


**Example 3:**

```
Input: head = [1]
Output: [1]
```

---

## 解法

這個方法跟我初時的想法差不多，但忍不住去偷瞄了一下 discuss，不過我神速的瞄了一眼，其實沒看到什麼，但「感受」到了端倪，就回來邊畫圖邊解題，就這樣解出來了，解法很難解釋，就是手跟著畫指標，一邊調整思路。

**心法：萬變不離其宗，調整指向而已。**


```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        dummy = ListNode(-1)
        dummy.next = head
        cur = dummy
        
        while cur.next and cur.next.next:
            fir = cur.next
            sec = cur.next.next
            cur.next = sec
            fir.next = sec.next
            sec.next = fir
            cur = cur.next.next
        
        return dummy.next
```

---

## 總結


將 [Lear: Linked List](https://leetcode.com/explore/learn/card/linked-list/) 完整練習完後，對於 Linked List 清晰了不少，有時只是欠缺一個完整的輪廓，耐著性子了解透徹便是。
