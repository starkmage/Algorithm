### 0~n-1中缺失的数字II

---

一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

示例 1:
```
输入: [0,1,3]
输出: 2
示例 2:

输入: [0,1,2,3,4,5,6,7,9]
输出: 8
```
---

#### 二分查找

如果不用二分查找，这道题就没啥意思了

``` js
var missingNumber = function(nums) {
  let len = nums.length
  // 当不缺时，输出排序下一个值
  if (nums[len - 1] === len - 1) return len
  let left = 0, right = len - 1
  while (left < right) {
    let center = Math.floor((left + right) / 2)
    if (center === nums[center]) left = center + 1
    else right = center
  }
  return left
};
```
