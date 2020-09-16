### 322.零钱兑换

---

给定不同面额的硬币 coins 和一个总金额 amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 -1。

示例 1:
```
输入: coins = [1, 2, 5], amount = 11
输出: 3 
解释: 11 = 5 + 5 + 1
```
示例 2:
```
输入: coins = [2], amount = 3
输出: -1
```

说明:
你可以认为每种硬币的数量是无限的。

---

#### 动态规划

我们用 dp[i] 表示 i 元最少需要用多少个硬币组成。初始 0 元需要 0 个硬币，所以 dp[0] = 0.

dp 中每个初始值我们设为 amount + 1，为什么这样呢？

其实不一定非得设为这个数字，这只是为了标记没有任何一种硬币组合能组成该金额，这也和最后的 return 条件判断对应。

在 coins[j] 小于总金额 i 的情况下，这个硬币才有可能用来组成总金额，所以：

动态转移方程：dp[i] = min(dp[i - coins[j]] + 1，dp[i])

dp[i] 就等于 i 减去该枚硬币金额后的金额由多少枚硬币组成，再加上 coins[j] 这个硬币就可以了

如果 dp[i - coins[j]] === amount + 1，那没关系，证明 dp[i] 也不能被组成，照样保持 amount + 1就好了

``` js
var coinChange = function(coins, amount) {
  // 填充这个数字的目的，结合最后一行代码看一下就明白了
  const dp = Array(amount + 1).fill(amount + 1)
  dp[0] = 0
  for (let i = 1; i < amount + 1; i++) {
    for (let j = 0; j < coins.length; j++) {
      if (coins[j] <= i) {
        dp[i] = Math.min(dp[i], dp[i - coins[j]] + 1)
      }
    }
  }
  return dp[amount] > amount ? -1 : dp[amount]
};
```
