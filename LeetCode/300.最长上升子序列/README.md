### 300.最长上升子序列

---

给定一个无序的整数数组，找到其中最长上升子序列的长度。

示例:
```
输入: [10,9,2,5,3,7,101,18]
输出: 4 
```
解释: 最长的上升子序列是 [2,3,7,101]，它的长度是 4。
说明:

可能会有多种最长上升子序列的组合，你只需要输出对应的长度即可。
你算法的时间复杂度应该为 O(n2) 。
进阶: 你能将算法的时间复杂度降低到 O(n log n) 吗?

---

#### 动态规划

注意，题目中说的子序列，并不一定是连续的子序列

方法1：动态规划
dp[i] = max(dp[j]) + 1

``` js
var lengthOfLIS = function(nums) {
  let len = nums.length
  if (len === 0) return 0
  const dp = Array(len).fill(1)
  for (let i = 1; i < len; i++) {
    for (let j = 0; j < i; j++) {
      if (nums[j] < nums[i]) dp[i] = Math.max(dp[i], dp[j] + 1)
    }
  }
  return Math.max(...dp)
};
```

方法2：二分查找
https://leetcode.cn/problems/longest-increasing-subsequence/solutions/1033432/dong-tai-gui-hua-he-er-fen-cha-zhao-lian-x7dh/

``` js
/**
 * @param {number[]} nums
 * @return {number}
 */
var lengthOfLIS = function(nums) {
  let output = 0
  const top = []

  for (const n of nums) {
    let left = 0
    let right = output

    while (left < right) {
      const mid = Math.floor((left + right) / 2)

      if (top[mid] >= n) {
        right = mid
      } else {
        left = mid + 1
      }
    }

    if (left === output) {
      output++
    }

    top[left] = n
  }

  return output
};
```
