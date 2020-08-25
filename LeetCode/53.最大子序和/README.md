### 53.最大子序和

---

给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

示例:
```
输入: [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```
进阶:

如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。

---

#### 思路

这道题和“剑指offer30题连续子数组的最大和”是一模一样的

动态规划的思想

用两个变量记录：max为最大和，sum为不断累加的和

如果sum>max了，则将max的值更新

如果sum<0了，则说明sum不再对后面求最大值有贡献，令sum=array[i]，重新开始累加

``` js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
  if (nums.length === 0) return
  let sum = nums[0]
  let max = nums[0]
  for (let i = 1; i < nums.length; i++) {
    if (sum < 0) {
      sum = nums[i]
    } else {
      sum += nums[i]
    }

    if (sum > max) {
      max = sum
    }
  }
  return max
};
```
