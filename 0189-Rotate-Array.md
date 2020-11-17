# 189. Rotate Array

## 題目描述


Given an array, rotate the array to the right by k steps, where k is non-negative.

Follow up:

- Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
- Could you do it in-place with O(1) extra space?





**Example 1:**:

```
Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

**Example 2:**:

```
Input: nums = [-1,-100,3,99], k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
```


--- 

## 一、解法一

```
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        l = len(nums)
        sub = nums[l - k:] # 1. 暫存 K 之後到 sub
        nums[:] = (sub + nums)[:l] # 2. sub + num，只取陣列前面，也就是 [5,6,7,1,2,3,4,5,6,7] 將最後 k 個 filter 掉
```

---

## 總結

還算順利想出來了。

