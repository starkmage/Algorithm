### 55.跳跃游戏

---

给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个位置。

示例 1:
```
输入: [2,3,1,1,4]
输出: true
解释: 我们可以先跳 1 步，从位置 0 到达 位置 1, 然后再从位置 1 跳 3 步到达最后一个位置。
```
示例 2:
```
输入: [3,2,1,0,4]
输出: false
解释: 无论怎样，你总会到达索引为 3 的位置。但该位置的最大跳跃长度是 0 ， 所以你永远不可能到达最后一个位置。
```
---

#### 思路

从后往前遍历，假设 i 可以跳到终点

对于 i - 1 来说，跳到 i 需要 1 步

而如果 i - 1 的值为 0，则 i - 1 为无价值的位置，不能跳到 i - 1（否则就出不去了！），则从 i - 2 跳到 i 需要 2 步，依次类推

两个值记录遍历过程，temp 为跳到下一个有价值的点需要的步数，flag记录成功或者失败

``` js
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var canJump = function(nums) {
  if (nums.length === 0 || nums.length === 1) return true
  let flag = true
  let temp = 1
  for (let i = nums.length - 2; i >= 0; i--) {
    if (nums[i] < temp) {
      flag = false
      temp++
    } else {
      flag = true
      temp = 1
    }
  }
  return flag
};
```
