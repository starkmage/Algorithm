### 416.分割等和子集

---

给定一个只包含正整数的非空数组。是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。

注意:

每个数组中的元素不会超过 100
数组的大小不会超过 200
示例 1:
```
输入: [1, 5, 11, 5]

输出: true

解释: 数组可以分割成 [1, 5, 5] 和 [11].
```
示例 2:
```
输入: [1, 2, 3, 5]

输出: false
```
解释: 数组不能分割成两个元素和相等的子集.

---

#### 动态规划

可以这么理解题目：给定数组 nums，是否存在一个子数组，该子数组的和等于 nums 元素和的一半。

我们用一个一维数组 dp 来记录题目的解，dp[i] 表示是否存在元素和为 i 的子数组。

对于 nums 中的每个数字 n 来说，都有选和不选两种选择，选的话问题变成 dp[i - n]，不选的话问题还是 dp[i]，所以：

```
dp[i] = dp[i - n] or dp[i]
```

看代码实现：

``` js
var canPartition = function(nums) {
  let sum = nums.reduce((total, value) => total + value)
  // 和为奇数，必然不行
  if (sum % 2 !== 0) return false
  sum = sum / 2
  const dp = Array(sum + 1).fill(false)
  dp[0] = true
  for (let n of nums) {
    for (let i = sum; i >= n; i--) {
      dp[i] = dp[i] || dp[i - n]
    }
  }
  return dp[sum]
};
```
