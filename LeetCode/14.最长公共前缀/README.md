### 14.最长公共前缀

---

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

示例 1:

输入: ["flower","flow","flight"]
输出: "fl"
示例 2:

输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。
说明:

所有输入只包含小写字母 a-z 。

---

#### 思路

``` js
var longestCommonPrefix = function(strs) {
  let len = strs.length
  if (len === 0) return ''
  if (len === 1) return strs[0]
  let res = strs[0].split(''), min = strs[0].length
  for (let i = 1; i < len; i++) {
    let char = strs[i], j = 0
    while (j < min && char[j] === res[j]) j++
    min = Math.min(min, j)
    if (min === 0) return ''
  }
  return res.slice(0, min).join('')
};
```
