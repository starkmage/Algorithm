### 581.最短无序连续子数组

---

给定一个整数数组，你需要寻找一个连续的子数组，如果对这个子数组进行升序排序，那么整个数组都会变为升序排序。

你找到的子数组应是最短的，请输出它的长度。

示例 1:
```
输入: [2, 6, 4, 8, 10, 9, 15]
输出: 5
解释: 你只需要对 [6, 4, 8, 10, 9] 进行升序排序，那么整个表都会变为升序排序。
```
说明 :

输入的数组长度范围在 [1, 10,000]。
输入的数组可能包含重复元素 ，所以升序的意思是<=。

---

#### 思路

从左到右循环，记录遍历过的最大值为 max，若 nums[i] < max, 则表明位置 i 需要调整, 循环结束，记录需要调整的最大位置 i 为 last；

同理，从右到左循环，记录遍历过的最小值为 min, 若 nums[i] > min, 则表明位置 i 需要调整，循环结束，记录需要调整的最小位置 i 为 first；

需要调整的长度即为 last - first + 1，注意，若 last === first，说明不需要调整，返回 0 即可，没有返回 1 的情况。

``` js
var findUnsortedSubarray = function(nums) {
  const len = nums.length
  if (len === 0 || len === 1) return 0
  let max = nums[0], min = nums[len - 1]
  let last = 0, first = 0
  // 从左到右遍历
  for (let i = 1; i < len; i++) {
    if (nums[i] < max) last = i
    if (nums[i] > max) max = nums[i]
  }
  // 从右到左遍历
  for (let j = len - 2; j >= 0; j--) {
    if (nums[j] > min) first = j
    if (nums[j] < min) min = nums[j]
  }
  // 要么不需要，要么长度至少为 2
  return first === last ? 0 : last - first + 1
};
```
