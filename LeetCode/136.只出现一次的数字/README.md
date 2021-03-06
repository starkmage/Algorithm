### 136.只出现一次的数字

---

给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

说明：

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

示例 1:
```
输入: [2,2,1]
输出: 1
```
示例 2:
```
输入: [4,1,2,1,2]
输出: 4
```
---

#### 思路

异或，两个相同的数字异或为0

这道题只有一个单独的数字，所以比较简单，“剑指offer-40.数组中只出现一次的数字”是这道题的加难版

``` js
var singleNumber = function(nums) {
  let res = 0
  //异或
  for (let item of nums) {
    res = res ^ item
  }
  return res
};
```
