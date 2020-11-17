# 189. Rotate Array


## 題目描述

There is a special square room with mirrors on each of the four walls.  Except for the southwest corner, there are receptors on each of the remaining corners, numbered 0, 1, and 2.

The square room has walls of length p, and a laser ray from the southwest corner first meets the east wall at a distance q from the 0th receptor.

Return the number of the receptor that the ray meets first.  (It is guaranteed that the ray will meet a receptor eventually.)


**Example 1:**:

```
Input: p = 2, q = 1
Output: 2
Explanation: The ray meets receptor 2 the first time it gets reflected back to the left wall.
```
(![](https://i.imgur.com/taqhcCR.png))

--- 

## 一、解法一

原理在於無限往右延伸鏡子，可看 [這篇文章](https://buptwc.com/2018/06/26/Leetcode-858-Mirror-Reflection/) 的解釋。

```
class Solution:
    def mirrorReflection(self, p: int, q: int) -> int:
        
        k = 1 # 1. 倍數
        while p * k % q != 0: k += 1 # 2. 找到 k
        
        if k % 2 == 0: # 3. 若 k 為偶數，則位於下方，也就是 0
            return 0
        else: # 4. 若 k 為奇數，則位於上方，可能為 1 或 2
            r = p * k / q # 5. 找到相對於 p 的倍數，若為偶數回傳 2，否則回傳 1
            if r % 2 == 0:
                return 2
            else:
                return 1
```

---

## 總結

還算順利想出來了。

