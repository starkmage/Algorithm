### 128.最长连续序列

---

给定一个未排序的整数数组，找出最长连续序列的长度。

要求算法的时间复杂度为 O(n)。

示例:
```
输入: [100, 4, 200, 1, 3, 2]
输出: 4
解释: 最长连续序列是 [1, 2, 3, 4]。它的长度为 4。
```
---

#### 思路

题目要求时间复杂度`O(n)`，那应该要用到 map 空间换时间了

key 存数字，value 存什么？

新存入的数字，如果它找到相邻的数，它希望从邻居数那里获取什么信息？

* 很显然它希望，左邻居告诉它左边能提供的连续长度，右邻居告诉它右边能提供的连续长度

* 加上它自己的长度，就有了自己处在的连续序列的长度

更新两端 value

* 同处一个连续序列的数字的value理应都相同，这是它们共同特征，但没有必要每个的value都是序列长度，只需要两端的数存序列的长度就好

* 因为靠的是两端和新数对接，序列是连续的，中间没有空位

* 序列的一端找到邻居后，将另一端对应的value更新为最新的序列长度

``` js
var longestConsecutive = function(nums) {
  let map = {}
  let max = 0
  for (let item of nums) {
    //只需要考虑不存在map[item]的情况
    if (map[item] === undefined) {
      let leftLen = map[item - 1] || 0
      let rightLen = map[item + 1] || 0
      let newLen = 1 + leftLen + rightLen
      map[item] = newLen
      //更新两端的长度,只需要更新两端就可以了
      map[item - leftLen] = newLen
      map[item + rightLen] = newLen
      //更新最大长度
      max = Math.max(max, newLen)
    }
  }
  return max
};
```
