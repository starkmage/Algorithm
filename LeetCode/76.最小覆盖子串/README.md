### 76.最小覆盖子串

---
给你一个字符串 S、一个字符串 T 。请你设计一种算法，可以在 O(n) 的时间复杂度内，从字符串 S 里面找出：包含 T 所有字符的最小子串。

示例：
```
输入：S = "ADOBECODEBANC", T = "ABC"
输出："BANC"
```

提示：

如果 S 中不存这样的子串，则返回空字符串 ""。
如果 S 中存在这样的子串，我们保证它是唯一的答案。

---

#### 滑动窗口

滑动窗口，和No.576基本一样

``` js
/**
 * @param {string} s
 * @param {string} t
 * @return {string}
 */
var minWindow = function(s, t) {
  if (s.length < t.length) {
    return ''
  }

  const strsMap = {}
  let counter = 0

  for (const str of t) {
    if (strsMap[str]) {
      strsMap[str]++
    } else {
      strsMap[str] = 1
      counter++
    }
  }

  let left = 0
  let output = ''

  for (let right = 0; right < s.length; right++) {
    const str = s[right]
    if (strsMap[str] !== undefined) {
      strsMap[str]--

      if (strsMap[str] === 0) {
        counter--
      }
    } 

    while (counter === 0) {
      if (right - left + 1 < output.length ||( output === '')) {
        output = s.slice(left, right + 1)
      }

      const leftStr = s[left]
      if (strsMap[leftStr] !== undefined) {
        strsMap[leftStr]++

        if (strsMap[leftStr] === 1) {
          counter++
        }
      }

      left++
    }
  }

  return output
};
```
