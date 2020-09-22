# 102. Binary Tree Level Order Traversal


## 題目描述

Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree `[3,9,20,null,null,15,7],`



```
    3
   / \
  9  20
    /  \
   15   7
```

return its level order traversal as:

```
[
  [3],
  [9,20],
  [15,7]
]
```

---

## 一、解法一：while + for

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
            
            if sub_res: # 4. 若陣列不為空，res.append
                res.append(sub_res)
                
        return res
```

---

## 總結

利用 While + For loop 很聰明，思路上很簡單，要想到卻很難，理解的同時好像又一秒轉彎忘記，大概就是天能的倒退開車吧。
