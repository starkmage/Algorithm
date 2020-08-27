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

核心思想：在 s 上滑动窗口，通过移动 right 指针不断扩张窗口。当窗口包含 t 全部所需的字符后，如果能收缩，我们就通过 left 收缩窗口直到得到最小窗口

具体细节看注释

``` js
/**
 * @param {string} s
 * @param {string} t
 * @return {string}
 */
var minWindow = function(s, t) {
  let slen = s.length
  let tlen = t.length
  if (slen < tlen) return ''
  let map = {}
  let missType = 0

  //首先统计s中的字符种类，和每个字符的个数
  for (let i = 0; i < tlen; i++) {
    let char = t[i]
    if (map[char] === undefined) {
      map[char] = 1
      missType++
    } else {
      map[char]++
    }
  }

  let left = 0
  let right = 0
  let start = 0
  let min = Number.MAX_VALUE
  for (right ; right < slen; right++) {
    let char = s[right]
    //当map中找到这个字符，这个字符需要的个数减1
    if (map[char] !== undefined) {
      map[char]--
    }
    //当一个字符需要的个数为0了，需要的种类减1
    if (map[char] === 0) {
      missType--
    }

    //当missType为0，证明找齐了t中的字符
    while (missType === 0) {
      if (right - left + 1 < min) {
        min = right - left + 1
        //记录最短字符串的起始位置
        start = left
      }
      //注意，map[left]原本可能是负数哦，比如s在这一段有5个'a'，而t中有3个'a'，那么map[a] = -2
      let char = s[left]
      if (map[char] !== undefined) map[char]++
      if (map[char] > 0) missType++
      left++
    }
  }
  //如果min一直没变，证明根本没找到
  if (min === Number.MAX_VALUE) return ''
  return s.slice(start, start + min)
};
```
