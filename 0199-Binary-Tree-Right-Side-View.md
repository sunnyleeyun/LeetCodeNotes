# 199. Binary Tree Right Side View


## 題目描述

Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.


**Example**:


```
Input: [1,2,3,null,5,null,4]
Output: [1, 3, 4]
Explanation:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```


--- 
## 一、解法一

提示：
1. Level order traversal
2. 只需要存每一層的最後一個為 res 即可

```
class Solution:
    def rightSideView(self, root: TreeNode) -> List[int]:
        if root is None:
            return []
        res = []
        queue = [root]
        
        while queue:
            sub_res = []
            for i in range(len(queue)):
                cur = queue.pop(0)
                if cur:
                    sub_res.append(cur.val)
                    queue.append(cur.left)
                    queue.append(cur.right)
            if sub_res:
                res.append(sub_res[-1])
            
        return res
```

---

## 總結

此題為 [Level Order Traversal](https://github.com/sunnyleeyun/LeetCodeNotes/blob/master/0102-Binary-Tree-Level%20Order-Traversal.md) 的變形
