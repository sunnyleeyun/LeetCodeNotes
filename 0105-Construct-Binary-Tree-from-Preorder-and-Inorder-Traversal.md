# 105. Construct Binary Tree from Preorder and Inorder Traversal

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

用上面的例子來分析：

```
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
首先根據 preorder 找到根節點是 3

然後根據根節點將 inorder 分成左子樹和右子樹
左子樹
inorder [9]

右子樹
inorder [15,20,7]

把相應的前序遍歷的數組也加進來
左子樹
preorder[9] 
inorder [9]

右子樹
preorder[20 15 7] 
inorder [15,20,7]

現在我們只需要構造左子樹和右子樹即可，成功把大問題化成了小問題
然後重復上邊的步驟繼續劃分，直到 preorder 和 inorder 都為空，返回 null 即可
```

可惜的是，我當時思考到了這階段，但沒能自己寫出來，其一是還沒能掌握遞迴的精髓，真的要寫 code 的時候總會卡在一個神秘角落，其二是對於 Tree 火侯總是差了點！滴水總會穿石的繼續加油吧～心路歷程先分享到這兒，咱們繼續解題。

我們只需要分別用兩指針，指向開頭與結束位置即可。**注意：範圍包括左邊界，但不包括右邊界。**

![](https://windliang.oss-cn-beijing.aliyuncs.com/105_3.jpg)

左子樹：

![](https://windliang.oss-cn-beijing.aliyuncs.com/105_4.jpg)

右子樹：

![](https://windliang.oss-cn-beijing.aliyuncs.com/105_5.jpg)

```
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        return self.helper(preorder, 0, len(preorder), inorder, 0, len(inorder))
        
    def helper(self, preorder: List[int], p_start: int, p_end: int, inorder: List[int], i_start: int, i_end: int) -> TreeNode:
        # Preorder 為空，直接返回 None
        if p_start == p_end:
            return None
        
        # 1. 由 preorder 找 root_val，並創建 root
        root_val = preorder[p_start] # 由 preorder 的 start 找到 root_val
        root = TreeNode(root_val) # 基於 root_val 產一個 root tree 出來，之後加上左右子樹，return root
        
        # 2. 從 root_val 找到 inorder 的 root_index 
        i_root_index = 0 # 也可以說是 inorder_root_index 縮寫
        for i in range(len(inorder)):
            if inorder[i] == root_val:
                i_root_index = i
                break
        
        # 3. 找到左邊界
        leftNum = i_root_index - i_start
        
        # 4. 替 root 遞迴 .left & .right 的子樹
        # left: (搭配上圖左子樹)
        #   preorder -> p_start + 1 (從 root index 往右移一格)
        #               p_start + leftNum + 1 (不包括右邊界，所以要 +1)
        #   inorder -> i_start
        #              i_root_index
        root.left = self.helper(preorder, p_start + 1, p_start + leftNum + 1, 
                                inorder, i_start, i_root_index)
                                
        # right: (搭配上圖右子樹)
        #   preorder -> p_start + leftNum + 1
        #               p_end
        #   inorder -> i_root_index + 1 (從 root_index 右移一格)
        #              i_end
        root.right = self.helper(preorder, p_start + leftNum + 1, p_end, 
                                 inorder, i_root_index + 1, i_end)
        return root
```

但這樣我們每次都要遍歷 inorder 的 root_index，可以調整成用一個 dictionary 儲存每個元素的值和下標。

```
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        # 0. 將 inorder 每個元素的值和下標儲存起來
        dict = {}
        for i in range(len(inorder)):
            dict[inorder[i]] = i
        return self.helper(preorder, 0, len(preorder), inorder, 0, len(inorder), dict)
        
    def helper(self, preorder: List[int], p_start: int, p_end: int, inorder: List[int], i_start: int, i_end: int, dict: {}) -> TreeNode:
        # Preorder 為空，直接返回 None
        if p_start == p_end:
            return None
        
        # 1. 由 preorder 找 root_val，並創建 root
        root_val = preorder[p_start]
        root = TreeNode(root_val)
        
        # 2. 從 root_val 找到 inorder 的 root_index 
        i_root_index = dict[root_val]
        
        leftNum = i_root_index - i_start
        
        # 3. 找到左邊界
        leftNum = i_root_index - i_start
        
        # 4. 替 root 遞迴 .left & .right 的子樹
        # left: (搭配上圖左子樹)
        #   preorder -> p_start + 1 (從 root index 往右移一格)
        #               p_start + leftNum + 1 (不包括右邊界，所以要 +1)
        #   inorder -> i_start
        #              i_root_index

        root.left = self.helper(preorder, p_start + 1, p_start + leftNum + 1, 
                                inorder, i_start, i_root_index, dict)
                                
        # right: (搭配上圖右子樹)
        #   preorder -> p_start + leftNum + 1
        #               p_end
        #   inorder -> i_root_index + 1 (從 root_index 右移一格)
        #              i_end
        root.right = self.helper(preorder, p_start + leftNum + 1, p_end, 
                                 inorder, i_root_index + 1, i_end, dict)
        return root
```

---

## 總結

遞迴跟理解 inorder 與 preorder 的應用。


reference: [105. Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.wang/leetcode-105-Construct-Binary-Tree-from-Preorder-and-Inorder-Traversal.html)
