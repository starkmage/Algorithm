### 494.目标和

---

给定一个非负整数数组，a1, a2, ..., an, 和一个目标数，S。现在你有两个符号 + 和 -。对于数组中的任意一个整数，你都可以从 + 或 -中选择一个符号添加在前面。

返回可以使最终数组和为目标数 S 的所有添加符号的方法数。

示例：
```
输入：nums: [1, 1, 1, 1, 1], S: 3
输出：5
解释：

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3
```
一共有5种方法让最终目标和为3。
 

提示：

数组非空，且长度不会超过 20 。
初始的数组的和不会超过 1000 。
保证返回的最终结果能被 32 位整数存下。

---

#### 动态规划

和“LeetCode-416.分割等和子集”非常接近

sum(P) 前面符号为+的集合；sum(N) 前面符号为减号的集合

所以题目可以转化为：
```
sum(P) - sum(N) = S 
=> sum(nums) + sum(P) - sum(N) = S + sum(nums)
=> 2 * sum(P) = S + sum(nums)        此处已经证明 S + sum(nums) 必须是偶数
=> sum(P) = (S + sum(nums)) / 2
```
因此题目转化为01背包，也就是能组合成容量为sum(P)的方式有多少种

dp[i] 代表的含义是从 nums 中取数相加和为i时有多少种取法。i = 0 时，就是说从 nums 中取数相加和为0时有几种取法，只有一种即一个数也不取，所以 dp[0] = 1

``` js
var findTargetSumWays = function(nums, S) {
  let sum = nums.reduce((total, val) => total + val)
  if (sum < S || (sum + S) % 2 !== 0) return 0
  let p = (sum + S) / 2
  let dp = Array(p + 1).fill(0)
  dp[0] = 1
  for (let value of nums) {
    for (let i = p; i >= value; i--) {
      dp[i] += dp[i - value]
    }
  }
  return dp[p]
};
```
