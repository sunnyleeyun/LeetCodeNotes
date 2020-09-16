# 98. Validate Binary Search Tree

## 題目描述

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

- The left subtree of a node contains only nodes with keys less than the node's key.
- The right subtree of a node contains only nodes with keys greater than the node's key.
- Both the left and right subtrees must also be binary search trees.


**Example 1:**

```
    2
   / \
  1   3

Input: [2,1,3]
Output: true
```



**Example 2:**

```
    5
   / \
  1   4
     / \
    3   6

Input: [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```


---

## 一、解法一：中序遍歷

看到題目想說用遞迴寫出來，想法上是「根節點大於左孩子小於右孩子」，但這會有問題，下面這個 case 不會過：
```
     10
    /  \
   5   15
      /  \
     6   20
```

第一次刷題的節奏就是想超過五分鐘沒有思路看答案，又對中序遍歷比較熟悉，因此先學習了以下解。

思路上是「中序遍歷順序為左孩子、根節點、右孩子」，而二分查找的性質是「左孩子小於根節點，根節點小於右孩子」，那如果我們將中序遍歷結果輸出，會得到一個從小到大的序列。

更進一步，我們只需要進行一次中序遍歷，把當前遍歷的結果和前一個遍歷結果值進行比較即可。


```
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        if root is None:
            return True
        
        stack = []
        cur, pre = root, None
        
        while cur or stack:
            while cur:
                stack.append(cur)
                cur = cur.left
            
            cur = stack.pop()
            if pre and pre.val >= cur.val: # 如果「pre != None」且「pre 值 大於 cur 值」-> 左 >= 右 -> False
                return False
            pre = cur
            cur = cur.right
        return True
```

---

## 總結

老樣子，學習前序、中序、後序遍歷，甚至是 DFS, BFS 的熟悉度與應變，這部分還在努力吸收中，`Done is better than none.` 先學習一個思路。

