### 34.在排序数组中查找元素的第一个和最后一个位置

---

给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。

你的算法时间复杂度必须是 O(log n) 级别。

如果数组中不存在目标值，返回 [-1, -1]。

示例 1:
```
输入: nums = [5,7,7,8,8,10], target = 8
输出: [3,4]
```
示例 2:
```
输入: nums = [5,7,7,8,8,10], target = 6
输出: [-1,-1]
```
---

#### 思路

题目要求时间复杂度`O(log n)`，那必然是二分查找

这道题和剑指offer的37题思路一模一样，只是返回的值不同而已

利用二分查找依次找到下界和上界即可

``` js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var searchRange = function(nums, target) {
  if (nums.length === 0) return [-1, -1]
  let res = [-1, -1]
  let left = 0
  let right = nums.length
  //寻找下界，下界为第一个等于target的值
  while (left < right) {
    let mid = left + Math.floor((right - left) / 2)
    if (nums[mid] < target) {
      left = mid + 1
    } else {
      right = mid
    }
  }
  if (nums[left] === target) res[0] = left
  left = 0
  right = nums.length
  //寻找上界,上界为第一个大于target的值
  //因为floor让mid靠近left，所以必须操作left变化，否则可能会无限循环
  while (left < right) {
    let mid = left + Math.floor((right - left) / 2)
    if (nums[mid] <= target) {
      left = mid + 1
    } else {
      right = mid
    }
  }
  if (nums[right - 1] === target) res[1] = right - 1
  return res
};
```
