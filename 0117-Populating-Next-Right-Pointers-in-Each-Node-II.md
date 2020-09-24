# 117. Populating Next Right Pointers in Each Node


## 題目描述

You are given a **perfect binary** tree where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}

```
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to NULL.


**Follow up:**

- You may only use constant extra space.
- Recursive approach is fine, you may assume implicit stack space does not count as extra space for this problem.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/02/15/117_sample.png)

```
Input: root = [1,2,3,4,5,null,7]
Output: [1,#,2,3,#,4,5,7,#]
Explanation: Given the above binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```


---

## 一、解法一：BFS

跟 [116 題](https://github.com/sunnyleeyun/LeetCodeNotes/blob/master/0116-Populating-Next-Right-Pointers-in-Each-Node.md) 一模一樣，一行程式碼都不需改。


```
class Solution:
    def connect(self, root: 'Node') -> 'Node':
        if root is None:
            return root
        queue = []
        queue.append(root)
        
        while queue:
            pre = None
            for i in range(len(queue)):
                cur = queue.pop(0)
                # 從第二個節點開始，將前一個節點 pre 指向當前節點
                if i > 0:
                    pre.next = cur
                pre = cur
                
                if cur.left:
                    queue.append(cur.left)
                if cur.right:
                    queue.append(cur.right)
        
        return root
```

---

## 總結

一模一樣的程式碼，當作重複練習，之後再回來學習更多思路。



