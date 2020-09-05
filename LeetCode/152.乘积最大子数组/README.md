### 152.乘积最大子数组

---

给你一个整数数组 nums ，请你找出数组中乘积最大的连续子数组（该子数组中至少包含一个数字），并返回该子数组所对应的乘积。

示例 1:
```
输入: [2,3,-2,4]
输出: 6
解释: 子数组 [2,3] 有最大乘积 6。
```
示例 2:
```
输入: [-2,0,-1]
输出: 0
解释: 结果不能为 2, 因为 [-2,-1] 不是子数组。
```
---

#### 思路

如果 nums 内有 0，则按 0 将 nums 分为若干段

如果不含 0，则分成以下两种情况：

1. 如果 nums 内有偶数个负数，则所有数相乘最大

2. 如果有奇数个负数，则最大乘积为“从左乘到最后一个负数之前”和“从右乘到第一个负数之后”中的一个

看起来要分成很多情况，实际上写起来不需要分情况，只需要遍反向历两次即可

``` js
var maxProduct = function(nums) {
  if (nums.length === 0) return null
  let max = nums[0]
  let temp = 1
  // 1. 左到右
  for (let value of nums) {
    temp = temp * value
    if (temp > max) max = temp
    if (value === 0) temp = 1
  }
  // 2. 右到左
  temp = 1
  for (let i = nums.length - 1; i >= 0; i--) {
    temp = temp * nums[i]
    if (temp > max) max = temp
    if (nums[i] === 0) temp = 1
  }
  return max
};
```
