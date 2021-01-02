# 266. Palindrome Permutation


## 題目描述

Given a string, determine if a permutation of the string could form a palindrome.


**Example 1:**

```
Input: "code"
Output: false
```


**Example 2:**

```
Input: "aab"
Output: true
```


**Example 3:**

```
Input: "carerac"
Output: true
```


---

## 解法

題目很簡單，基本用 Set 就搞定。

```
class Solution:
    def canPermutePalindrome(self, s: str) -> bool:
        t = set()
        for i in range(len(s)):
            if s[i] in t: # 1. Set 已有該值 -> remove
                t.remove(s[i])
            else: # 1. Set 無該值 -> add
                t.add(s[i])
        return len(t) == 0 or len(t) == 1 # set 最後長度為 0 或 1 皆可能為 Palindrome
```



---


## 總結

題目很簡單，set 輕鬆解。


