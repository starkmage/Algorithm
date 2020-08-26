### 62.不同路径

---

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

问总共有多少条不同的路径？

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/robot_maze.png)

例如，上图是一个7 x 3 的网格。有多少可能的路径？

示例 1:
```
输入: m = 3, n = 2
输出: 3
解释:
从左上角开始，总共有 3 条路径可以到达右下角。
1. 向右 -> 向右 -> 向下
2. 向右 -> 向下 -> 向右
3. 向下 -> 向右 -> 向右
```
示例 2:
```
输入: m = 7, n = 3
输出: 28
```
---

#### 动态规划

核心方程 dp[i][j] = dp[i-1][j] + dp[i][j-1]

因为当机器人在 [i-1][j] 处，只需要向下走一下就可以到达[i][j]，在 [i][j-1]只需要向右走一下就可以，所以到 [i][j] 的走法等于这两者之和

这跟跳台阶的问题非常像

``` js
/**
 * @param {number} m
 * @param {number} n
 * @return {number}
 */
var uniquePaths = function(m, n) {
  //生成一个 m X n 全为1的二维数组
  //因为第一行和第一列的走法只有1种
  //初始为1比较方便
  let item = Array(n).fill(1)
  let dp = Array(m).fill([...item])
  for (let i = 1; i < m; i++) {
    for (let j = 1; j < n; j++) {
      dp[i][j] = dp[i-1][j] + dp[i][j-1]
    }
  }
  return dp[m-1][n-1]
};
```
