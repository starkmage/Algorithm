### 79.单词搜索

---

给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

示例:
```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "ABCCED", 返回 true
给定 word = "SEE", 返回 true
给定 word = "ABCB", 返回 false
```

提示：
```
board 和 word 中只包含大写和小写英文字母。
1 <= board.length <= 200
1 <= board[i].length <= 200
1 <= word.length <= 10^3
```
---

#### 思路

回溯算法，与“剑指offer-65.矩阵中的路径”基本一样

``` js
/**
 * @param {character[][]} board
 * @param {string} word
 * @return {boolean}
 */
var exist = function(board, word) {
  let m = board.length
  let n = board[0].length
  //记录是否走过
  let flag = Array(m).fill(0).map(item => Array(n).fill(false))
  //不确定是从哪个地方开始，所以需要遍历
  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (board[i][j] === word[0]) {
        if(help(board, m, n, i, j, word, 0, flag)) return true
      }
    }
  }
  return false
};

function help(board, m, n, i, j, word, k, flag) {
  //剪枝：1.越界；2.走过了；3.不相等
  if (i < 0 || i >= m || j < 0 || j >= n || flag[i][j] || board[i][j] !== word[k]) {
    return false
  }
  //走到头了，匹配成功
  if (k === word.length - 1) return true
  //标记走过了
  flag[i][j] = true
  //四个方向递归
  if (help(board, m, n, i + 1, j, word, k + 1, flag) ||
    help(board, m, n, i - 1, j, word, k + 1, flag) ||
    help(board, m, n, i, j + 1, word, k + 1, flag) ||
    help(board, m, n, i, j - 1, word, k + 1, flag)) return true
  //上面递归失败，证明此路不通，就当没来过这里，因为还要进行下一个起点轮次的递归
  flag[i][j] = false
  return false
}
```
