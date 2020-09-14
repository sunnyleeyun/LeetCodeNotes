# 144. Binary Tree Preorder Traversal

## 題目描述

Given a binary tree, return the preorder traversal of its nodes' values.

**Example:**

```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,2,3]
```

**Follow up**: Recursive solution is trivial, could you do it iteratively?

---

## 基本概念

前序遍歷順序為：V->L->R

---

## 一、解法一：Recursive 遞迴

最基本的解法，遞歸公式＆VLR，也就是創建一個 helper，在裡面 **印 val -> 左 -> 右**

```
class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        self.helper(root, res)
        return res
        
    def helper(self, root: TreeNode, res: List[int]):
        if root:
            res.append(root.val)
            self.helper(root.left, res)
            self.helper(root.right, res)
```

---

## 二、解法二：Iterative 迭代


![](https://github.com/MisterBooo/LeetCodeAnimation/raw/master/0144-Binary-Tree-Preorder-Traversal/Animation/Animation.gif)

#### 過程
（前序遍歷 V->L->R）

1. 根節點 Push 到線中
2. 循環檢測「線是否為空」，若不為空，則取出線頂元素，打印
3. 看其右子節點是否存在，若存在，Push 到線中
4. 接著看其右子節點是否存在，若存在，Push 到線中

*註：先壓右子樹的原因是因為「線是後進先出（LIFO）」*


```
class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        stack = []
        res = []
        if root is None:
            return res
        
        stack.append(root) # 1. 根節點 Push 到線中
        while stack: # 2.1 循環檢測「線是否為空」
            cur = stack.pop() 
            if cur:
                res.append(cur.val) # 2.2 若不為空，則取出線頂元素，打印
                if cur.right: # 3. 看其右子節點是否存在，若存在，Push 到線中
                    stack.append(cur.right)
                if cur.left: # 4. 接著看其右子節點是否存在，若存在，Push 到線中
                    stack.append(cur.left)
        
        return res
```

---

## 總結

遞迴方式基本的一定要把握住，迭代方式用圖像搭配比較容易找出思路，記得先壓右子樹因為「線為後進先出」。

