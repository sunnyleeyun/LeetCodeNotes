# 222. Count Complete Tree Nodes


## 題目描述

Given a *complete* binary tree, count the number of nodes.

Note:

[Definition of a complete binary tree from Wikipedia](https://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees):
In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.



**Example**:


```
Input: 
    1
   / \
  2   3
 / \  /
4  5 6

Output: 6
```


--- 
## 一、解法一

提示
* 想到 tree 就要想到遞迴
* 如果有 perfect binary tree -> 公式 `pow(2, h) - 1`
* 結合以上兩個

```
class Solution:
    def countNodes(self, root: TreeNode) -> int:
        
        # 1. 分別尋找 left & right 找到 Height -> l1, l2
        left = root
        l1 = 0
        while left: 
            l1 += 1
            left = left.left
            
        right = root
        l2 = 0
        while right: 
            l2 += 1
            right = right.right
            
        if l1 == l2: # 2. 若 l1 == l2 -> perfect binary tree，公式處理
            return pow(2, l1) - 1
        else: # 3. 遞迴處理
            return self.countNodes(root.right) + self.countNodes(root.left) + 1
```

---

## 總結

第一個要
