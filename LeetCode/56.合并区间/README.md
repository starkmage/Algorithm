### 56.合并区间

---

给出一个区间的集合，请合并所有重叠的区间。

示例 1:
```
输入: intervals = [[1,3],[2,6],[8,10],[15,18]]
输出: [[1,6],[8,10],[15,18]]
解释: 区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].
```
示例 2:
```
输入: intervals = [[1,4],[4,5]]
输出: [[1,5]]
解释: 区间 [1,4] 和 [4,5] 可被视为重叠区间。
```
提示：
```
intervals[i][0] <= intervals[i][1]
```
---
#### 思路

1. 将数组按照左边界排序

2. 用 j 记录 res 的下标

3. 当 intervals[i][0] <= res[j-1][1] 时，更新 res[j-1][1]，注意取 res[j-1][1], intervals[i][1] 中的最大值

4. 当 intervals[i][0] > res[j-1][1]，证明范围与前面不重叠，直接压入 res，j 也需要加 1

5. 本题不需要考虑深拷贝的问题

``` js
/**
 * @param {number[][]} intervals
 * @return {number[][]}
 */
var merge = function(intervals) {
  if (intervals.length === 0) return []
  intervals.sort((a, b) => a[0] - b[0])
  let res = [intervals[0]]
  let j = 1
  for (let i = 1; i < intervals.length; i++) {
    if (intervals[i][0] <= res[j-1][1]) {
      res[j-1][1] = Math.max(res[j-1][1], intervals[i][1])
    } else {
      res.push(intervals[i])
      j++
    }
  }
  return res
}; 
```
