### 215.数组中的第K个最大的元素

---

在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

示例 1:
```
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
```
示例 2:
```
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```
说明:

你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。

---

#### 最小堆

其实最简单的方法是排序，下面给出的是最小堆的方法

这道题和“剑指offer-29.最小的K个数”很类似，具体可以参考[这里](http://www.conardli.top/docs/dataStructure/%E5%A0%86/%E5%A0%86.html)

``` js
var findKthLargest = function(nums, k) {
  if (nums.length === 0) return
  createMinHeap(nums, k)
  for (let i = k; i < nums.length; i++) {
    if (nums[i] >= nums[0]) {
      [nums[0], nums[i]] = [nums[i], nums[0]]
      adjustMinHeap(nums, 0, k)
    }
  }
  return nums[0]
};

// 建立一个 k 长度的小顶堆，堆顶即为第 k 个最大的元素
function createMinHeap(nums, len) {
  // 堆的最后一个非叶子节点
  let last = Math.floor(len / 2) - 1
  for (let i = last; i >= 0; i--) {
    adjustMinHeap(nums, i, len)
  }
}

function adjustMinHeap(nums, index, len) {
  for (let i = 2 * index + 1; i < len; i = 2 * i + 1) {
    // 找到两个子节点中较小的那个
    if (i + 1 < len && nums[i + 1] < nums[i]) {
      i++
    }
    // 把较小的节点移到上方
    if (nums[i] <= nums[index]) {
      [nums[i], nums[index]] = [nums[index], nums[i]]
      index = i
    } else {
      break
    }
  }
}
```
