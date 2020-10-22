### 33.搜索旋转排序数组

---


假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 -1 。

你可以假设数组中不存在重复的元素。

你的算法时间复杂度必须是 O(log n) 级别。

示例 1:
```
输入: nums = [4,5,6,7,0,1,2], target = 0
输出: 4
```
示例 2:
```
输入: nums = [4,5,6,7,0,1,2], target = 3
输出: -1
```
---

#### 思路

看到要求时间复杂度O(log(n))，必然是二分查找

``` js
var search = function(nums, target) {
  if (nums.length === 0) return -1
  if (nums.length === 1) return nums[0] === target ? 0 : -1
  let left = 0
  let right = nums.length - 1
  while(left < right) {
    let mid = left + Math.floor((right - left)/2)
    if (nums[mid] === target) {
      return mid
    } else {
      //1. 如果mid在前半升序段
      if (nums[mid] >= nums[0]) {
        //1.1 target在left和mid之间，包括left
        if (nums[mid] > target && nums[left] <= target) {
          right = mid - 1
        } else {  //1.2 target在mid右侧
          left = mid + 1
        }
      } else {  //2. 如果mid在后半升序段
        //2.1 target在mid和right之间，包括right
        if (nums[mid] < target && nums[right] >= target) {
          left = mid + 1
        } else {  //2.2 target在mid左侧
          right = mid - 1
        }
      }
    }
  }
  return nums[left] === target ? left : -1
};
```
