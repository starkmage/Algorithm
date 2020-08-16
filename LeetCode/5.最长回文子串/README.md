### 5.最长回文子串

---

给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

示例 1：
```
输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。
```

示例 2：
```
输入: "cbbd"
输出: "bb"
```
---

#### 思路

中心扩展法

``` js
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function (s) {
  let res = ''
  let len = s.length
  for (let i = 0; i < 2 * len - 1; i++) {
    let left = Math.floor(i / 2)
    let right = left + i % 2
    let temp = ''
    while (left >= 0 && right < len && s[left] === s[right]) {
      if (left === right) {
        temp = s[left]
      } else {
        temp = s[left] + '' + temp + '' + s[right]
      }
      left--
      right++
    }
    if (temp.length > res.length) {
      res = temp
    }
  }
  return res
};
```
