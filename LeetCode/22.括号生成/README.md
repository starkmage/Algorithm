### 22.括号生成

---
数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。

示例：
```
输入：n = 3
输出：[
       "((()))",
       "(()())",
       "(())()",
       "()(())",
       "()()()"
     ]
```
---

#### 思路

利用DFS + 少量的剪枝，剪枝的一个重要条件为右括号的数目大于左括号的

``` js
/**
 * @param {number} n
 * @return {string[]}
 */
var generateParenthesis = function (n) {
  if (n <= 0) return []
  let res = []
  help(0, 0, n, '', res)
  return res
};

function help(left, right, n, temp, res) {
  //重点！当右括号的数目大于左括号，不允许！
  if (left > n || right > n || right > left) return
  if (left === n && right === n) {
    res.push(temp)
    return
  }
  help(left+1, right, n, temp + '(', res)
  help(left, right+1, n, temp + ')', res)
}
```
