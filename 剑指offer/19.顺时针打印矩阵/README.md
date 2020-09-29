### 19.顺时针打印矩阵

---

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下4 X 4矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.

---

* 思路

顺时针打印就是按圈数循环打印，一圈包含两行或者两列，在打印的时候会出现某一圈中只包含一行，要判断从左向右打印和从右向左打印的时候是否会出现重复打印，同样只包含一列时，要判断从上向下打印和从下向上打印的时候是否会出现重复打印的情况。

2020年9月29日更新，之前的方法太绕了，现在更新一种更简单的思路。

---

``` JS
var spiralOrder = function(matrix) {
  if (matrix.length === 0) return []
  let top = 0, bottom = matrix.length - 1
  let left = 0, right = matrix[0].length - 1
  const res = []
  const size = matrix.length * matrix[0].length
  while (res.length !== size) {
    // 左到右
    for (let j = left; j <= right; j++) res.push(matrix[top][j])
    top++
    // 上到下
    for (let i = top; i <= bottom; i++) res.push(matrix[i][right])
    right--
    // 防止只剩一行或者一列出现重复
    if (res.length === size) break
    // 右到左
    for (let j = right; j >= left; j--) res.push(matrix[bottom][j])
    bottom--
    // 下到上
    for (let i = bottom; i >= top; i--) res.push(matrix[i][left])
    left++
  }
  return res
};
```
