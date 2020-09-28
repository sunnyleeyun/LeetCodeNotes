# 129. Sum Root to Leaf Numbers


## 題目描述

Given a binary tree containing digits from `0-9` only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path `1->2->3` which represents the number 123.

Find the total sum of all root-to-leaf numbers.

**Note**: A leaf is a node with no children.

**Example1**:


```
Input: [1,2,3]
    1
   / \
  2   3
Output: 25
Explanation:
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.
Therefore, sum = 12 + 13 = 25.
```


**Example2**:


```
Input: [4,9,0,5,1]
    4
   / \
  9   0
 / \
5   1
Output: 1026
Explanation:
The root-to-leaf path 4->9->5 represents the number 495.
The root-to-leaf path 4->9->1 represents the number 491.
The root-to-leaf path 4->0 represents the number 40.
Therefore, sum = 495 + 491 + 40 = 1026.
```

---

## 一、解法一：DFS

深度遍歷，也就是得到一個解後，紀錄當下的解，再找下一個解，再統一用一個 `sum` 參數存起來、return 就好。

```
class Solution:
    sum = 0
    def sumNumbers(self, root: TreeNode) -> int:
        if root is None:
            return 0
        curSum = root.val
        self.dfs(root, curSum)
        return self.sum
    
    def dfs(self, root: TreeNode, curSum: int):
        if root.left is None and root.right is None:
            self.sum += curSum
            return
        
        if root.left:
            self.dfs(root.left, curSum * 10 + root.left.val)
            
        if root.right:
            self.dfs(root.right, curSum * 10 + root.right.val)
```

---

## 總結

方法不難，可惜的是不知道是否好幾天沒解題覺得面目可憎解不出來，還是還沒抓到那個感覺，反正就是火侯不夠沒自己寫出來，但看了別人的思路理解得挺快的，應該快抓到頭了吧！

BTW 回去看了 [Binary Tree: Traveral（尋訪）](http://alrightchiu.github.io/SecondRound/binary-tree-traversalxun-fang.html)，再稍微理了一下前序、中序、後序遍歷等等，發現題目的三個都不是，而是 Level-Order，這邊稍微整理一下：

**Pre-Order**:

`A B D E G H C F I`

根節點在最前面，VLR

![](https://github.com/alrightchiu/SecondRound/blob/master/content/Algorithms%20and%20Data%20Structures/Tree%20series/BinaryTree_fig/Traversal/f18.png?raw=true)


**In-Order**

`D B G E H A F I C`

根節點會在中間（除非左右子樹為空），LVR

![](https://github.com/alrightchiu/SecondRound/blob/master/content/Algorithms%20and%20Data%20Structures/Tree%20series/BinaryTree_fig/Traversal/f19.png?raw=true)

**Post-Order**

`D G H E B I F C A`

根節點會在最後，LRV

![](https://github.com/alrightchiu/SecondRound/blob/master/content/Algorithms%20and%20Data%20Structures/Tree%20series/BinaryTree_fig/Traversal/f20.png?raw=true)
