### 16.最接近的三数之和

---

给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

示例：
```
输入：nums = [-1,2,1,-4], target = 1
输出：2
解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。
``` 

提示：
```
3 <= nums.length <= 10^3
-10^3 <= nums[i] <= 10^3
-10^4 <= target <= 10^4
```

---

#### 思路

和15题三数之和一样的思路

``` js
var threeSumClosest = function(nums, target) {
  let len = nums.length
  nums.sort((a, b) => a - b)
  let min = Infinity
  let z, x, c
  for (let i = 0; i < len; i++) {
    let left = i + 1, right = len - 1
    while (left < right) {
      let sum = nums[i] + nums[left] + nums[right]
      if (Math.abs(target - sum) < min) {
        min = Math.abs(target - sum)
        z = i
        x = left
        c = right
      }
      if (sum < target) left++
      else if (sum > target) right--
      else return sum
      
    }
  }
  return nums[z] + nums[x] + nums[c]
};
```
