### 49.字母异位词分组

---

给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。

示例:
```
输入: ["eat", "tea", "tan", "ate", "nat", "bat"]
输出:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```
说明：

所有输入均为小写字母

不考虑答案输出的顺序

---

#### 思路

哈希表法，对每个字符串进行排序，哈希表记录出现的字符组合以及它在结果数组中的下标，当遇到重复的将其压入结果数组指定的下标子数组中

``` js
/**
 * @param {string[]} strs
 * @return {string[][]}
 */
var groupAnagrams = function(strs) {
  if (strs.length === 0) return []
  let res = []
  let map = {}
  let index = 0
  for (let s of strs) {
    let temp = s.split('').sort().join('')
    if (map[temp] !== undefined) {
      res[map[temp]].push(s)
    } else {
      map[temp] = index
      res.push([s])
      index++
    }
  }
  return res
};
```
