# 845. Longest Mountain in Array


## 題目描述

Let's call any (contiguous) subarray B (of A) a mountain if the following properties hold:

- `B.length >= 3`
- There exists some `0 < i < B.length - 1` such that `B[0] < B[1] < ... B[i-1] < B[i] > B[i+1] > ... > B[B.length - 1]`


(Note that B could be any subarray of A, including the entire array A.)

Given an array A of integers, return the length of the longest mountain. 

Return 0 if there is no mountain.



**Example 1:**:

```
Input: [2,1,4,7,3,2,5]
Output: 5
Explanation: The largest mountain is [1,4,7,3,2] which has length 5.
```

**Example 2:**:

```
Input: [2,2,2]
Output: 0
Explanation: There is no mountain.
```


--- 

## 一、解法一

* Hint: 
    * 找到 Peek
    * left, right

```
class Solution:
    def longestMountain(self, A: List[int]) -> int:
        if len(A) < 3: return 0
        
        res = 0
        for i in range(1, len(A) - 1): # 1. 從 1 ~ n - 2，因為最左跟最右不可能為 Peek
            if A[i - 1] < A[i] and A[i] > A[i + 1]: # 2. 找到 Peek，由其為中心找左右邊界
                l = i - 1
                r = i + 1
                while l > 0 and A[l - 1] < A[l]: l -= 1
                while r < len(A) - 1 and A[r + 1] < A[r]: r += 1
                res = max(res, r - l + 1)
                    
        return res
```

---

## 總結

自己嘗試的方式超時了 O(n^2)，學習到的思路是找峰頂再找邊界。
