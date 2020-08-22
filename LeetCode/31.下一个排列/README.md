### 31.下一个排列

---
实现获取下一个排列的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。

如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。

必须原地修改，只允许使用额外常数空间。

以下是一些例子，输入位于左侧列，其相应输出位于右侧列。
```
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```
---

#### 思路

1. 其实就是从数组倒着查找，找到nums[i-1] 比nums[i]小的时候，就将nums[i-1]跟nums[i]到nums[nums.length - 1]当中找到一个最小的比nums[i]大的元素交换

2. 交换后，再把nums[i]到nums[nums.length-1]排序

3. 区间nums[i]到nums[nums.length-1]是降序的，所以排序的时候可以方便的两两交换完成排序

``` js
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var nextPermutation = function(nums) {
  let len = nums.length
  if (len === 0 || len === 1) return nums
  let flag = 0

  //1.从后往前寻找第一个出现nums[i] > nums[i-1]的地方
  for (let i = len - 1; i > 0; i--) {
    if (nums[i] > nums[i-1]) {
      flag = i
      break
    }
  }

  //2.如果没找到，证明nums是完全降序的
  if (flag === 0) return nums.reverse()

  //3.把nums[flag-1]和flag后面中第一个大于nums[flag-1]的值交换
  let j = len - 1
  while (nums[j] <= nums[flag-1]) {
    j--
  }
  swap(nums, flag-1, j)
  
  //4.flag后面是降序的，需要排成升序，才是字典序
  //因为是降序的，所以直接两两交换即可
  while (flag < len) {
    swap(nums, flag, len-1)
    flag++
    len--
  }
  return nums
};

function swap(nums, i, j) {
  let temp = nums[i]
  nums[i] = nums[j]
  nums[j] = temp
}
```
