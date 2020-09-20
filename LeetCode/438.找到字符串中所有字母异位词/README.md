### 438.找到字符串中所有字母异位词

---

给定一个字符串 s 和一个非空字符串 p，找到 s 中所有是 p 的字母异位词的子串，返回这些子串的起始索引。

字符串只包含小写英文字母，并且字符串 s 和 p 的长度都不超过 20100。

说明：

字母异位词指字母相同，但排列不同的字符串。
不考虑答案输出的顺序。
示例 1:
```
输入:
s: "cbaebabacd" p: "abc"

输出:
[0, 6]
```
解释:
起始索引等于 0 的子串是 "cba", 它是 "abc" 的字母异位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的字母异位词。
 示例 2:
```
输入:
s: "abab" p: "ab"

输出:
[0, 1, 2]
```
解释:
起始索引等于 0 的子串是 "ab", 它是 "ab" 的字母异位词。
起始索引等于 1 的子串是 "ba", 它是 "ab" 的字母异位词。
起始索引等于 2 的子串是 "ab", 它是 "ab" 的字母异位词。

---

#### 思路

滑动窗口的思路，和“LeetCode-76.最小覆盖子串”的思路基本一样

``` js
var findAnagrams = function(s, p) {
  const res = []
  // needs 记录 p 的字符数量，windows 记录窗口里可以供 p 使用的字符数量
  const needs = {}, windows = {}
  let match = 0, needsLen = 0
  // 遍历 p 记录在 needs 里
  for (let char of p) {
    if (needs[char] !== undefined) {
      needs[char]++
    } else {
      needs[char] = 1
      needsLen++
    }
  }
  // 窗口的两侧
  let left = 0, right = 0
  while (right < s.length) {
    let char1 = s[right]
    // 只记录 p 需要的
    if (needs[char1]) {
      windows[char1] ? windows[char1]++ : windows[char1] = 1
      // 匹配全的种类 + 1
      if (windows[char1] === needs[char1]) match++
    }
    // 窗口右移
    right++
    // 如果种类匹配全了，数量大于等于了
    while(match === needsLen) {
      // 窗口里的字符数量和 p 的一样
      if (right - left === p.length) res.push(left)
      let char2 = s[left]
      if (needs[char2]) {
        windows[char2]--
        if (windows[char2] < needs[char2]) match--
      }
      left++
    }
  }
  return res
};
```
