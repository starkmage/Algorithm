### 15.三数之和

---

给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。 

示例：
```
给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```
---

#### 排序+双指针

时间复杂度O(n^2)

1. 为了方便去重，我们首先将数组排序

2. 对数组进行遍历，取当前遍历的数nums[i]为一个基准数，遍历数后面的数组为寻找数组

3. 在寻找数组中设定两个起点，最左侧的left(i+1)和最右侧的right(length-1)

4. 判断nums[i] + nums[left] + nums[right]是否等于0，如果等于0，加入结果，并分别将left和right移动一位

5. 如果结果大于0，将right向左移动一位，向结果逼近

6. 如果结果小于0，将left向右移动一位，向结果逼近

7. 注意始终保持去重

``` js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var threeSum = function (nums) {
  const result = []
  nums.sort((a, b) => a - b)
  for (let i = 0; i < nums.length; i++) {
    //跳过重复数字
    if (nums[i] === nums[i - 1]) continue
    let left = i + 1
    let right = nums.length - 1
    while (left < right) {
      let sum = nums[i] + nums[left] + nums[right]
      if (sum === 0) {
        result.push([nums[i], nums[left], nums[right]])
        left++
        right--
        //跳过重复数字
        while (nums[left] === nums[left - 1]) {
          left++
        }
        while (nums[right] === nums[right + 1]) {
          right--
        }
      } else if (sum > 0) {
        right--
      } else {
        left++
      }
    }
  }
  return result
}
```
