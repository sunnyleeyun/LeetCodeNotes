# 103. Binary Tree Zigzag Order Traversal


## 題目描述

Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).


For example:
Given binary tree `[3,9,20,null,null,15,7],`



```
    3
   / \
  9  20
    /  \
   15   7
```

return its zigzag level order traversal as:

```
[
  [3],
  [20,9],
  [15,7]
]
```

---

## 一、解法一：while + for

這題跟 102 題一樣，只差在偶數層做翻轉。

![](https://camo.githubusercontent.com/d77b97df0e728b820d122715ebf1446c5e0ba7ea/68747470733a2f2f626c6f672d313235373132363534392e636f732e61702d6775616e677a686f752e6d7971636c6f75642e636f6d2f626c6f672f78756f716f2e676966)

```
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        res = []
        queue = [] # 應用 Queue: FIFO
        queue.append(root)
        
        while queue: # 1. Queue 不為空就持續遍歷
            sub_res = []
            for i in range(len(queue)): # 2. 當前元素個數
                cur = queue.pop(0) # 3. Pop 第 0 個
                if cur: # 3. 同時直接將下一層儲存進 Queue
                    sub_res.append(cur.val)
                    queue.append(cur.left)
                    queue.append(cur.right)
            
            if sub_res: # 4. 若陣列不為空，res.append（偶數層做翻轉）
                if len(res) % 2 == 0: # 原本為偶數層，下一層便是奇數層
                    res.append(sub_res)
                else: 
                    sub_res.reverse()
                    res.append(sub_res)
            return res
```

---

## 總結

昨天才寫完 102 題，103 幾乎一模一樣，很開心自己寫了出來一題（痛哭流涕，而且代表昨天的題也懂了 :]
