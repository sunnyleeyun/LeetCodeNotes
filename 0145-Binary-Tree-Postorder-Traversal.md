# 145. Binary Tree Postorder Traversal

## 題目描述

Given the root of a binary tree, return the postorder traversal of its nodes' values.


**Example 1:**

```
   1
    \
     2
    /
   3

Input: root = [1,null,2,3]
Output: [3,2,1]
```



**Example 2:**

```
Input: root = []
Output: []
```


**Example 3:**

```
Input: root = [1]
Output: [1]
```



**Example 4:**

```
Input: root = [1,2]
Output: [2,1]
```

**Example 5:**

```
Input: root = [1,null,2]
Output: [2,1]
```

**Follow up**: Recursive solution is trivial, could you do it iteratively?

---

## 基本概念

前序遍歷：VLR （[0144 題](https://github.com/sunnyleeyun/LeetCodeNotes/blob/master/0144-Binary-Tree-Preorder-Traversal.md)）

中序遍歷：LVR （[0094 題](https://github.com/sunnyleeyun/LeetCodeNotes/blob/master/0094-Binary-Tree-Inorder-Traversal.md)）

後序遍歷：LRV （[0145 題](https://github.com/sunnyleeyun/LeetCodeNotes/blob/master/0145-Binary-Tree-Postorder-Traversal.md)）

*註：<L：Left；R：Right；V：Value>*

上面三題，本位一體，搭配一起服用。

碰到這類問題，直覺使用 Recursive 公式解，進一步使用 Iterative 解。

詳細概念說明：http://alrightchiu.github.io/SecondRound/binary-tree-traversalxun-fang.html

---

## 一、解法一：Recursive 遞迴

最基本的解法，遞歸公式＆LRV，也就是創建一個 helper，在裡面 **左 -> 右 -> 印 val**

```
class Solution:
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        self.helper(root, res)
        return res
        
    def helper(self, root: TreeNode, res: List[int]):
        if root:
            self.helper(root.left, res)
            self.helper(root.right, res)
            res.append(root.val)
```

---

## 二、解法二：Iterative 迭代


![](https://github.com/MisterBooo/LeetCodeAnimation/raw/master/0145-Binary-Tree-Postorder-Traversal/Animation/Animation.gif)

#### 過程
（後序遍歷：L->R->V）

1. 根節點 Push 到線中
2. 循環檢測「線是否為空」
3. 看其左子節點是否存在，若存在，Push 到線中
4. 接著看其右子節點是否存在，若存在，Push 到線中
5. 如果線頂點「沒有左右子節點」，或者「左子節點為 Head」，或者「右子節點是 Head」：取出線頂元素，「逆序」打印

*註：和前序遍歷不一樣，前序遍歷先壓右子樹，因為 LIFO；這裡先將左節點入線(3)，再將右節點入線(4)，因為我們在最後要「逆序」添加節點值(5)*


```
class Solution:
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        stack = []
        if root is None:
            return res
        
        stack.append(root) # 1. 根節點 Push 到線中
        while stack: # 2. 循環檢測「線是否為空」
            cur = stack.pop()
            if cur:
                if cur.left:
                    stack.append(cur.left) # 3. 看其左子節點是否存在，若存在，Push 到線中
                if cur.right:
                    stack.append(cur.right) # 4. 接著看其右子節點是否存在，若存在，Push 到線中
                res.insert(0, cur.val) # 5. 如果線頂點「沒有左右子節點」，或者「左子節點為 Head」，或者「右子節點是 Head」：取出線頂元素，「逆序」打印
        return res
```

---

## 總結

遞迴方式基本的一定要把握住，迭代方式用圖像搭配比較容易找出思路，記得後序遍歷與前序遍歷不一樣，前序遍歷先壓右子樹因為 LIFO，後序遍歷先壓左子樹因為逆序添加節點。

