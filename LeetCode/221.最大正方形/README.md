### 221.最大正方形

---

在一个由 0 和 1 组成的二维矩阵内，找到只包含 1 的最大正方形，并返回其面积。

示例:
```
输入: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

输出: 4
```
---

#### 动态规划

dp[i][j]表示以第i行第j列为右下角所能构成的最大正方形边长, 则递推式为: 

dp[i][j] = 1 + min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1]);

![](https://assets.leetcode-cn.com/solution-static/221/221_fig1.png)

``` js
var maximalSquare = function(matrix) {
  let max = 0
  let m = matrix.length
  if (m === 0) return 0
  let n = matrix[0].length
  let dp = Array(m).fill(0).map(item => Array(n).fill(0))
  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (matrix[i][j] == 1) {
        if (i === 0 || j === 0) {
          dp[i][j] = 1
        } else {
          dp[i][j] = 1 + Math.min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1])
        }
        max = Math.max(max, dp[i][j])
      }
    }
  }
  return max * max
};
```
