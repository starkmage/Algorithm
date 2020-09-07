### 169.多数元素

---

给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

示例 1:
```
输入: [3,2,3]
输出: 3
```
示例 2:
```
输入: [2,2,1,1,1,2,2]
输出: 2
```
---

#### 思路

这个题和“剑指offer-28.数组中出现次数超过一半的数字”一样，更简单，因为题目描述中确定一定有多数元素，不需要再进行检验

这里只给出最优的候选法，还有map法和排序法

``` js
var majorityElement = function(nums) {
  let res = nums[0]
  let count = 1
  for (let i = 1; i < nums.length; i++) {
    nums[i] === res ? count++ : count--
    if (count === 0) {
      res = nums[i]
      count = 1
    }
  }
  return res
};
```
