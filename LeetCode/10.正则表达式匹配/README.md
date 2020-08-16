### 10.正则表达式匹配

---

给你一个字符串 s 和一个字符规律 p，请你来实现一个支持 '.' 和 '*' 的正则表达式匹配

'.' 匹配任意单个字符

'*' 匹配零个或多个前面的那一个元素

所谓匹配，是要涵盖 整个 字符串 s的，而不是部分字符串

说明:

s 可能为空，且只包含从 a-z 的小写字母。

p 可能为空，且只包含从 a-z 的小写字母，以及字符 . 和 *

---

#### 思路

和剑指offer52题完全一样，可以去看那道题的注释

``` js
/**
 * @param {string} s
 * @param {string} p
 * @return {boolean}
 */
var isMatch = function(s, p) {
  if (s.length === 0 && p.length === 0) return true
  if (s.length !== 0 && p.length === 0) return false
  return matchHelp(s, 0, p, 0)
};

function matchHelp(s, i, p ,j) {
  if (i === s.length && j === p.length) return true
  if (i !== s.length && j === p.length) return false
  //如果p中下一个字符不是*
  if (p[j+1] !== '*') {
    if (i < s.length && (s[i] === p[j] || p[j] === '.')) {
      return matchHelp(s, i+1, p, j+1)
    } else {
      return false
    }
  }
  //p中下一个字符是*
  else {
    if (i < s.length && (s[i] === p[j] || p[j] === '.')) {
      return matchHelp(s, i+1, p, j) ||
        matchHelp(s, i, p, j+2) 
    } else {
      return matchHelp(s, i, p, j+2)
    }
  }
}
```
