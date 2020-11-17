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
  if (strs.length === 0) return ''
  if (strs.length === 1) return strs[0]
  const flag = strs[0].split('')
  let m = flag.length, min = m
  for (let i = 1; i < strs.length; i++) {
    let j = 0, temp = 0
    while (j < strs[i].length && j < m && strs[i][j] === flag[j]) {
      temp++
      j++
    }
    min = Math.min(min, temp)
    if (min === 0) return ''
  }
  return flag.slice(0, min).join('')
};
```
