### 78.子集

---

给定一组不含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。

说明：解集不能包含重复的子集。

示例:
```
输入: nums = [1,2,3]
输出:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```
---

#### 思路

遍历，遇到一个数就把所有子集加上该数组成新的子集，遍历完毕即是所有子集

``` js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsets = function(nums) {
  //注意放一个空子数组
  let res = [[]]
  for (let n of nums) {
    res.forEach(item => {
      res.push(item.concat(n))
    })
  }
  
  return res
};
```
