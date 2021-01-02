# 1640. Check Array Formation Through Concatenation


## 題目描述

You are given an array of distinct integers arr and an array of integer arrays pieces, where the integers in pieces are distinct. Your goal is to form arr by concatenating the arrays in pieces in any order. However, you are not allowed to reorder the integers in each array pieces[i].

Return true if it is possible to form the array arr from pieces. Otherwise, return false.

**Example 1:**

```
Input: arr = [85], pieces = [[85]]
Output: true
```


**Example 2:**

```
Input: arr = [15,88], pieces = [[88],[15]]
Output: true
Explanation: Concatenate [15] then [88]
```


**Example 3:**

```
Input: arr = [49,18,16], pieces = [[16,18,49]]
Output: false
Explanation: Even though the numbers match, we cannot reorder pieces[0].
```


**Example 4:**

```
Input: arr = [91,4,64,78], pieces = [[78],[4,64],[91]]
Output: true
Explanation: Concatenate [91] then [4,64] then [78]
```


**Example 5:**

```
Input: arr = [1,3,5,7], pieces = [[2,4,6,8]]
Output: false
```

---

## 解法一

自己寫出來的解法，Time Complexity 為 O(N^2)


```
class Solution:
    def canFormArray(self, arr: List[int], pieces: List[List[int]]) -> bool:
        i = 0
        while i < len(arr):
            for j in range(len(pieces)):
                if not pieces[j] or arr[i] != pieces[j][0]:
                    if j == len(pieces) - 1:
                        return False
                    continue
                # arr[i] == pieces[j][0]
                c = len(pieces[j])
                if arr[i] == pieces[j][0] and arr[i:i+c] == pieces[j]:
                    i += c
                    break
                else:
                    return False
        return True
```

---

## 解法二

Solution 裡面 Hashmap 的解法，Time Complexity 降為 O(N)

![](https://leetcode.com/problems/check-array-formation-through-concatenation/Figures/5554/5554_4.png)

```
class Solution:
    def canFormArray(self, arr: List[int], pieces: List[List[int]]) -> bool:
        n = len(arr)
        d = { p[0]: p for p in pieces }
        i = 0
        while i < n:
            if arr[i] not in d:
                return False
            p = d[arr[i]]
            for val in p:
                if val != arr[i]:
                    return False
                i += 1
                
        return True
```


---


## 總結

題目不難，很高興自己有餘力尋找不止一種解法。

