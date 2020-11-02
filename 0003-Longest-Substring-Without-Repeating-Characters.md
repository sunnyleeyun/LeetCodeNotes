# 3. Longest Substring Without Repeating Characters


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
