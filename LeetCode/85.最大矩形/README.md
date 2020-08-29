### 85.最大矩形

---

给定一个仅包含 0 和 1 的二维二进制矩阵，找出只包含 1 的最大矩形，并返回其面积。

示例:
```
输入:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
输出: 6
```
---

#### 思路

这道题其实就是84题的进阶版

对每一行都求出每个元素对应的高度，这个高度就是该列上该行上方连续1的长度，然后对每一行都更新一次最大矩形面积

本质上是对矩阵中的每行，均依次执行84题的算法

``` js
/**
 * @param {character[][]} matrix
 * @return {number}
 */
var maximalRectangle = function(matrix) {
  if (matrix.length === 0) return 0
  let m = matrix.length
  let n = matrix[0].length
  let heights = Array(n).fill(0)
  let max = 0
  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (matrix[i][j] === '0') {
        //当为0，同一列上面的1也没用了，因为相当于柱被割断了（不是连续的）
        heights[j] = 0
      } else {
        heights[j] = heights[j] + 1
      }
    }
    max = Math.max(max, help(heights))
  }
  return max
};

function help(heights) {
  heights.push(0)
  let stack = []
  let max = 0
  for (let i = 0; i < heights.length; i++) {
    while (stack.length && heights[i] < heights[stack[stack.length - 1]]) {
      let index = stack.pop()
      if (stack.length === 0) {
        max = Math.max(max, heights[index] * i)
      } else {
        max = Math.max(max, heights[index] * (i - stack[stack.length - 1] - 1))
      }
    }
    stack.push(i)
  }
  heights.pop()
  return max
}
```
