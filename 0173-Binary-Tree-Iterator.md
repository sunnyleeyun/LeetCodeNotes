# 173. Binary Search Tree Iterator


## 題目描述

Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.

Calling `next()` will return the next smallest number in the BST.


**Example**:

![](https://assets.leetcode.com/uploads/2018/12/25/bst-tree.png)

```
BSTIterator iterator = new BSTIterator(root);
iterator.next();    // return 3
iterator.next();    // return 7
iterator.hasNext(); // return true
iterator.next();    // return 9
iterator.hasNext(); // return true
iterator.next();    // return 15
iterator.hasNext(); // return true
iterator.next();    // return 20
iterator.hasNext(); // return false
```


--- 
## 一、解法一

提示：
1. 中序遍歷
2. queue, FIFO


```
class BSTIterator:
    queue = [] # 1. 新增一個陣列，FIFO

    def __init__(self, root: TreeNode):
        self.inorder(root) # 2. inorder method 處理好 queue
    
    def next(self) -> int:
        """
        @return the next smallest number
        """
        return self.queue.pop(0) # 3. next 即是 queue pop(0)

    def hasNext(self) -> bool:
        """
        @return whether we have a next smallest number
        """
        return self.queue # 4. queue 是否為空判斷
        
    def inorder(self, root): 
        if root is None:
            return
        self.inorder(root.left)
        self.queue.append(root.val)
        self.inorder(root.right)
```

---

## 總結

整個關鍵便在於有沒有想到這是 inorder 的變形。
