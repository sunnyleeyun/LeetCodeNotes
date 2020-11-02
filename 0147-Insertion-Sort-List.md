# 147. Insertion Sort List


## 題目描述

Sort a linked list using insertion sort.

![](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)

Algorithm of Insertion Sort:

1. Insertion sort iterates, consuming one input element each repetition, and growing a sorted output list.
2. At each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list, and inserts it there.
3. It repeats until no input elements remain.


**Example 1:**:

```
Input: 4->2->1->3
Output: 1->2->3->4
```

**Example 2:**:

```
Input: -1->5->3->4->0
Output: -1->0->3->4->5

```


--- 
## 一、解法一

提示
* 看到 ListNode 就想到 dummy


1. dummy 預設 ListNode
2. cur = head 並將 dummy.next 指向 head（最後 ans 便可得 dummy.next）
3. 當前 val <= next val，cur 往右移
4. 否則《現在要處理 cur.next，將其移到正確位置，並將指標重新指向》
    1. 暫存 cur.next 到 temp（下一步會將 cur.next 指標移掉，先暫存起來）
    2. cur.next 先指到 cur.next.next（再往下移一個，接著要將 temp 放到正確的地方）
    3. 將 dummy 暫存到 prev（所以我們又回到頭了）
    4. 當 prev.next 的值 <= temp 的值，往右移
    5. 處理完後，我們得知 temp 要放在 prev.next 之前，因此 temp.next = prev.next
    6. 並將 prev.next 指向 temp

[Youtube 解析](https://www.youtube.com/watch?v=N1VVLLan6S0)：文字表達簡直像繞口令，這個影片解釋得非常清楚，若有機會(?)我也來畫個 gif


```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def insertionSortList(self, head: ListNode) -> ListNode:
        dummy = ListNode(0)
        cur = head
        dummy.next = head
        
        while cur and cur.next:
            if cur.val <= cur.next.val:
                cur = cur.next // 3. 當前 val <= next val，cur 往右移
            else:
                temp = cur.next // 4.1. 暫存 cur.next 到 temp（下一步會將 cur.next 指標移掉，先暫存起來）
                cur.next = cur.next.next // 4.2. cur.next 先指到 cur.next.next（再往下移一個，接著要將 temp 放到正確的地方）
                prev = dummy // 4.3. 將 dummy 暫存到 prev（所以我們又回到頭了）
                while prev.next.val <= temp.val:
                    prev = prev.next // 4.4. 當 prev.next 的值 <= temp 的值，往右移
                temp.next = prev.next // 4.5. 處理完後，我們得知 temp 要放在 prev.next 之前，因此 temp.next = prev.next
                prev.next = temp // 4.6. 並將 prev.next 指向 temp
                
        return dummy.next
```

---

## 總結

這次邊畫圖邊跟著講解學習，終於播雲見日的感覺，但還是有一點點沒完全搞懂，即是「為什麼 dummy 不用再指向 prev（如 4.6 之後）」，我這邊猜測是前面已經獲得了 prev 的位址便可以直接用了吧？歡迎指教。# 3. Longest Substring Without Repeating Characters


## 題目描述

Given a string `s`, find the length of the longest substring without repeating characters.

**Example 1:**:

```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

**Example 2:**:

```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

```

**Example 3:**:

```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```


**Example 4:**:

```
Input: s = ""
Output: 0
```

--- 
## 一、解法一

提示
* 雙指針
* left 只能往右移
* hashmap



```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if len(s) == 0: return 0
        
        dict = {}
        left = 0
        ans = 0
        
        for i in range(len(s)): # i 為右指針
            if s[i] in dict:
                left = max(left, dict[s[i]] + 1) # KEY: left 只能往右移
            
            if i - left + 1 > ans:
                ans = i - left + 1
            
            dict[s[i]] = i
            
        return ans
```

時間複雜度：O(n)
空間複雜度：O(n)

---


## 解法二

同樣是雙指針，這裡使用 Set，左右指針皆只能往右移

```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        set_s = set()
        ans, l, r = 0, 0, 0
        
        while l < len(s) and r < len(s):
            if s[r] not in set_s: # 該 char 尚未存在於 set 中，新增 char 至 set，右指針右移，更新 ans
                set_s.add(s[r])
                r += 1
                ans = max(ans, r - l)
            else: # 當右指針碰到同樣的 char，從 set 裡面移除左指針 char 的值，左指針往右移
                set_s.remove(s[l])
                l += 1
                
        return ans
```


---

## 總結

雙指針的應用，個人偏向第一種解法，對我來說較為直觀。
