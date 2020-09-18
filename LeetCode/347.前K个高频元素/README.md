### 347.前K个高频元素

---

给定一个非空的整数数组，返回其中出现频率前 k 高的元素。

示例 1:
```
输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
```
示例 2:
```
输入: nums = [1], k = 1
输出: [1]
```

提示：

你可以假设给定的 k 总是合理的，且 1 ≤ k ≤ 数组中不相同的元素的个数。
你的算法的时间复杂度必须优于 O(n log n) , n 是数组的大小。
题目数据保证答案唯一，换句话说，数组中前 k 个高频元素的集合是唯一的。
你可以按任意顺序返回答案。

---

#### 思路

这种统计频率的问题，当然要想到 map 法，只不过这个题有点绕，具体的思路已经在代码中注释了

``` js
var topKFrequent = function(nums, k) {
  // 1. map存储 数字：出现次数 的键值对
  const map = {}
  for (let value of nums) {
    if (map[value] !== undefined) {
      map[value]++
    } else {
      map[value] = 1
    }
  }
  // 2. temp下标 i 即为出现次数为i，tem[i]为出现i次的数字们
  const temp = []
  for (let key in map) {
    let value = map[key]
    if (temp[value]) {
      temp[value].push(key)
    } else {
      temp[value] = [key]
    }
  }
  // 3. 从尾到头遍历 temp，可得到前 K 频次的数字
  const res = []
  for (let i = temp.length - 1; i >= 0 && res.length < k; i--) {
    if (temp[i]) {
      res.push(...temp[i])
    }
  }
  return res
};
```
