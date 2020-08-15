### 1.两数之和

---

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

---

#### 思路

暴力法很简单，时间复杂度O(n^2)

用map空间换时间，时间复杂度O(n)，空间复杂度O(n)

使用一个map将遍历过的数字存起来，值作为key，下标作为value

对于每一次遍历：

1. 取map中查找是否有key为target-nums[i]的值

2. 如果取到了，则条件成立，返回

3. 如果没有取到，将当前值作为key，下标作为值存入map

``` js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
  const map = {}
  if (nums.length < 2) return []
  for (let i = 0; i < nums.length; i++) {
    let need = target - nums[i]
    if (map[need] !== undefined) {
      return [map[need], i]
    } else {
      map[nums[i]] = i
    }
  }
  return []
};
```
