# 98. Construct Binary Tree from Preorder and Inorder Traversal

## 題目描述

Given preorder and inorder traversal of a tree, construct the binary tree.

Note:
You may assume that duplicates do not exist in the tree.

For example, given


```
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
```

Return the following binary tree:

```
    3
   / \
  9  20
    /  \
   15   7
```

---

## 一、解法一：遞迴


```
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        return self.helper(preorder, 0, len(preorder), inorder, 0, len(inorder))
    
    def helper(self, preorder: List[int], p_start: int, p_end: int, inorder: List[int], i_start: int, i_end: int) -> TreeNode:
        if p_start == p_end:
            return None
        
        root_val = preorder[p_start]
        root = TreeNode(root_val)
        
        i_root_index = 0
        for i in range(i_start, i_end):
            if root_val == inorder[i]:
                i_root_index = i
                break
        leftNum = i_root_index - i_start
        
        root.left = self.helper(preorder, p_start + 1, p_start + leftNum + 1, inorder, i_start, i_root_index)
        root.right = self.helper(preorder, p_start + leftNum + 1, p_end, inorder, i_root_index + 1, i_end)
        return root
```

---

## 總結

老樣子，學習前序、中序、後序遍歷，甚至是 DFS, BFS 的熟悉度與應變，這部分還在努力吸收中，`Done is better than none.` 先學習一個思路。

