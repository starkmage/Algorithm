### 3.无重复字符的最长子串

---


给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

示例 1:
```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

示例 2:
```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```
示例 3:
```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

---

#### map方法

看到这种类型的题目，除暴力法外，必然首先想到的就是创建一个map数据结构以空间换时间

* 以s[i]为key，i为value存入

* 用start记录试图寻找的最长字符串的开始位置

* 当map内有重复的s[i]时，请注意，这个s[i]可能在start之前，所以需要和start进行对比

``` js
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
  let max = 0
  let map = {}
  let start = 0
  for (let i = 0; i < s.length; i++) {
    if (map[s[i]] !== undefined) {
      start = Math.max(map[s[i]] + 1, start)
    }
    map[s[i]] = i
    max = Math.max(max, i - start + 1)
  }
  return max
};
```

#### 滑动窗口

* 记录两个指针，左指针为子串开始，右指针为子串结束（不包括右指针）

* 在每一步的操作中，我们会将左指针向右移动一格，表示 我们开始枚举下一个字符作为起始位置

* 然后我们可以不断地向右移动右指针，但需要保证这两个指针对应的子串中没有重复的字符

* 在移动结束后，这个子串就对应着以左指针开始的，不包含重复字符的最长子串。我们记录下这个子串的长度

* 使用set数据结构记录子串字符

* 不如map方法好理解，但是性能更优

``` js
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
  let set = new Set()
  let max = 0
  let right = 0
  for (let i = 0; i < s.length; i++) {
    if (i !== 0) {
      //左指针右移一格，删除一个字符
      set.delete(s[i-1])
    }
    //右指针进行遍历
    while (right < s.length && !set.has(s[right])) {
      set.add(s[right])
      right++
    }
    //此时right已经有重复的了，所以子串右下标应该为right-1
    max = Math.max(max, right - i)
  }
  return max
};
```


