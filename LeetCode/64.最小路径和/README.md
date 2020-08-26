### 64.最小路径和

---

给定一个包含非负整数的 m x n 网格，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

说明：每次只能向下或者向右移动一步。

示例:
```
输入:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 7
解释: 因为路径 1→3→1→1→1 的总和最小。
```
---

#### 动态规划

这道题的思想和62题完全一样

``` js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var minPathSum = function(grid) {
  let m = grid.length
  if (m === 0) return 0
  //如果是一维数组
  if (!Array.isArray(grid[0])) {
    return grid.reduce((total, value) => total + value, 0)
  }
  let n = grid[0].length
  //第一行的数值
  for (let k = 1; k < n; k++) {
    grid[0][k] += grid[0][k-1]
  }
  //第一列的数值
  for (let k = 1; k < m; k++) {
    grid[k][0] += grid[k-1][0]
  }
  for (let i = 1; i < m; i++) {
    for (let j = 1; j < n; j++) {
      grid[i][j] += Math.min(grid[i-1][j], grid[i][j-1])
    }
  }
  return grid[m-1][n-1]
};
```
