# 82. Remove Duplicates from Sorted List II



## 題目描述

Given the head of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list sorted as well.



**Example 1:**
![](https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg)
```
Input: head = [1,2,3,3,4,4,5]
Output: [1,2,5]
```


**Example 2:**
![](https://assets.leetcode.com/uploads/2021/01/04/linkedlist2.jpg)
```
Input: head = [1,1,1,2,3]
Output: [2,3]
```


---

## 解法


注意要移除掉所有數

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        dummy = ListNode(-1)
        dummy.next = head
        cur = dummy
        while cur.next and cur.next.next:
            if cur.next.val == cur.next.next.val:
                val = cur.next.val
                while cur.next and cur.next.val == val:
                    cur.next = cur.next.next
            else:
                cur = cur.next
        
        return dummy.next
```



---


## 總結

確保兩個至少兩個數。


