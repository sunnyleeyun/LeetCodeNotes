# 94. Binary Tree Inorder Traversal


## 題目描述

Given a binary tree, return the inorder traversal of its nodes' values.

**Example:**

```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,3,2]
```


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

## 解法一：Recursive 遞迴

最基本的解法，遞歸公式＆LVR，也就是創建一個 helper，在裡面 **左 -> 印 val -> 右**

- 終止條件：當前節點為空
- 函數內：調用左節點，打印當前節點，再遞迴調用右節點


```
# Python
class Solution:
def inorderTraversal(self, root: TreeNode) -> List[int]:
    res = []
    self.helper(root, res)
    return res

def helper(self, root: TreeNode, res: List[int]):
    if root:
        self.helper(root.left, res)
        res.append(root.val)
        self.helper(root.right, res)
```

> 時間複雜度：O(n)；
> 空間複雜度：O(h)，h 為樹高

---

## 解法二：Iterative 迭代

迭代法在思路上比較難想通，「線」的特性是 **先進後出（FILO）**，我們將左子樹的節點壓線，找不到左子樹時，線頂就是最底層的左子樹，出線打印出來；接著轉向右子樹父節點，繼續遍歷父節點的左子樹並壓線，以此循環。

#### 過程

1. 壓線根節點
2. 遍歷左子樹，壓線，直到左子樹為空
3. 出線線頂元素，打印
4. 轉向右子樹，重複 1, 2, 3 步驟

下圖展現了具體例子，來源 [94. Binary Tree Inorder Traversal 解法二 栈](https://leetcode.wang/leetCode-94-Binary-Tree-Inorder-Traversal.html#%E8%A7%A3%E6%B3%95%E4%BA%8C-%E6%A0%88) 

```
        1
      /   \
     2     3
    / \   /
   4   5 6

 push   push   push   pop     pop    push     pop     pop 
|   |  |   |  |_4_|  |   |   |   |  |   |    |   |   |   |  
|   |  |_2_|  |_2_|  |_2_|   |   |  |_5_|    |   |   |   |
|_1_|  |_1_|  |_1_|  |_1_|   |_1_|  |_1_|    |_1_|   |   |
ans                  add 4   add 2           add 5   add 1
[]                   [4]     [4 2]           [4 2 5] [4 2 5 1]
 push   push   pop          pop 
|   |  |   |  |   |        |   |  
|   |  |_6_|  |   |        |   |  
|_3_|  |_3_|  |_3_|        |   |
              add 6        add 3
              [4 2 5 1 6]  [4 2 5 1 6 3]

```

也可以由以下圖解分析，來源 [LeetCodeAnimation](https://github.com/MisterBooo/LeetCodeAnimation/blob/master/0094-Binary-Tree-Inorder-Traversal/Article/0094-Binary-Tree-Inorder-Traversal2.md)：

![](https://github.com/MisterBooo/LeetCodeAnimation/raw/master/0094-Binary-Tree-Inorder-Traversal/Animation/Animation2.gif)



```
# Python
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        stack, cur = [], root
        while cur or stack:
            while cur:
                stack.append(cur)
                cur = cur.left
            cur = stack.pop()
            res.append(cur.val)
            cur = cur.right
        
        return res
```

> 時間複雜度：O(n)；
> 空間複雜度：O(n)

---

## 總結

樹的基本概念：前序、中序、後序要搞清楚，遞迴公式法輕鬆破解基本題。中序的迭代方式重點整理：把東西往左堆，當都找不到左子樹了，再一個一個打印出來，看右子樹中的左子樹 etc... 重複這個步驟。
