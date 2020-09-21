### 560.和为K的子数组

---

给定一个整数数组和一个整数 k，你需要找到该数组中和为 k 的连续的子数组的个数。

示例 1 :
```
输入:nums = [1,1,1], k = 2
输出: 2 , [1,1] 与 [1,1] 为两种不同的情况。
```
说明 :

数组的长度为 [1, 20,000]。
数组中元素的范围是 [-1000, 1000] ，且整数 k 的范围是 [-1e7, 1e7]。

---

#### 思路

利用 map 法，map 存储的是 key 为 nums 数组中从头逐加的和 sum，value 为 sum 出现的次数

所以，如果存在 map[sum - k]，证明从求出和为 sum - k 的位置到 i 位置这个连续子数组，和为 k

``` js
var subarraySum = function(nums, k) {
  let count = 0, sum = 0
  // 为什么设 0: 1呢，因为 sum - k === 0，则说明 sum 自己就是一个结果
  const map = {0: 1}
  for (let n of nums) {
    sum += n
    if (map[sum - k]) count += map[sum - k]
    map[sum] ? map[sum]++ : map[sum] = 1
  }
  return count
};
```
