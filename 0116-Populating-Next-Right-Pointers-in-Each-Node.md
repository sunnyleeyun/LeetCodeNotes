# 116. Populating Next Right Pointers in Each Node


## 題目描述

You are given a **perfect binary** tree where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}

```
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to NULL.


**Follow up:**

- You may only use constant extra space.
- Recursive approach is fine, you may assume implicit stack space does not count as extra space for this problem.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/02/14/116_sample.png)

```
Input: root = [1,2,3,4,5,6,7]
Output: [1,#,2,3,#,4,5,6,7,#]
Explanation: Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```


---

## 一、解法一：BFS

首先，Perfect Binary Tree 就是滿二叉樹，這些一大堆樹的專有名詞要記得。

說來慚愧，看了 N 次回頭還是有點模糊。在學習方面一直不是很會記憶這些，感受起來特別死的東西，好比最近在學法文，單字方面特別弱，分明練了不少次，背誦起來仍是特別拙劣，往往用奇形怪狀的記憶法才有辦法背起來，哎呀不說了勤能補拙最終能內化成自己的一部分，咱們繼續。

我們先來分析一下題目，挺懊惱的第一次看新題多了個概念，比如這裡是多了個 next，我就頭暈目眩的，連題目都看不懂怎麼解題啊！（氣氣氣！狂揍兔子）總是得提醒自己不著急，又不是天才，新的東西不懂是正常的，扛著、扛著！

所以，白話文來說：
- 給一個**滿二叉樹**，每個節點多一個 `next` 指針，然後將所有的 `next` 指針指向它的「右邊節點」，*並且要求空間複雜度是 `O(1)`（這個解法暫時不管這個條件，先解出來理解一個解法之後再加強）*

---

那在開始之前，插個懶人包一下：
- BFS（Breadth-First Search）：廣度優先搜索
- DFS（Depth-First Search）：深度優先搜索

＊註：可以到 [【小馬的資結演算法秘笈】(7) 在演算法中常見的BFS, DFS是什麼?](https://ithelp.ithome.com.tw/articles/10231191#:~:text=%E6%BC%94%E7%AE%97%E6%B3%95%E9%A0%98%E5%9F%9F%E4%B8%AD%EF%BC%8C%E6%9C%89,%E6%B7%B1%E5%BA%A6%E5%84%AA%E5%85%88%E6%90%9C%E7%B4%A2%E7%9A%84%E7%B0%A1%E7%A8%B1) 初步了解，他的形容很白話很簡單。

---

我們這邊用的是 BFS，也就是廣度優先搜索，應用了跟 [102 題](https://github.com/sunnyleeyun/LeetCodeNotes/blob/master/0102-Binary-Tree-Level%20Order-Traversal.md) 幾乎一樣的方式：`while + for`（這個解法特別得我心做起來順手），做了一點點改變，咱們看 code。


```
class Solution:
    def connect(self, root: 'Node') -> 'Node':
        if root is None:
            return root
        queue = []
        queue.append(root)
        
        while queue:
            pre = None
            for i in range(len(queue)):
                cur = queue.pop(0)
                # 從第二個節點開始，將前一個節點 pre 指向當前節點
                if i > 0:
                    pre.next = cur
                pre = cur
                
                if cur.left:
                    queue.append(cur.left)
                if cur.right:
                    queue.append(cur.right)
        
        return root
```

---

## 總結

我們先學了一個最簡單的方式，也就是 [102 題](https://github.com/sunnyleeyun/LeetCodeNotes/blob/master/0102-Binary-Tree-Level%20Order-Traversal.md)，目前好幾題都用同樣的解法，可惜的是還沒完全符合條件「空間複雜度是 `O(1)`」，不過這我們之後再回來學習新思慮並重複加深記憶。



