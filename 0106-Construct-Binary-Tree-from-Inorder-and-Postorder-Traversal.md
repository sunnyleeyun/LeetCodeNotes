# 106. Construct Binary Tree from Inorder and Postorder Traversal


## 題目描述

Given inorder and postorder traversal of a tree, construct the binary tree.

Note:
You may assume that duplicates do not exist in the tree.

For example, given


```
inorder = [9,3,15,20,7]
postorder = [9,15,7,20,3]
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

跟 105 題解法一樣

```
class Solution:
    def buildTree(self, inorder: List[int], postorder: List[int]) -> TreeNode:
        dict = {}
        for i in range(len(inorder)):
            dict[inorder[i]] = i
        return self.helper(inorder, 0, len(inorder), postorder, 0, len(postorder), dict)
        
    def helper(self, inorder: List[int], i_start: int, i_end: int, postorder: List[int], p_start: int, p_end: int, dict: {}) -> TreeNode:
        
        if p_start == p_end:
            return None
        
        root_val = postorder[p_end - 1]
        root = TreeNode(root_val)
        i_root_index = dict[root_val]
        leftNum = i_root_index - i_start
        root.left = self.helper(inorder, i_start, i_root_index, 
                                postorder, p_start, p_start + leftNum, dict)
        root.right = self.helper(inorder, i_root_index + 1, i_end, 
                                 postorder, p_start + leftNum, p_end - 1, dict)
        return root
```

---

## 總結

雖然概念一樣，但解題似乎是一個手感，總是覺得不是特別順手。
