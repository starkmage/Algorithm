### 75.颜色分类

---

给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

注意:
不能使用代码库中的排序函数来解决这道题。

示例:
```
输入: [2,0,2,1,1,0]
输出: [0,0,1,1,2,2]
```
---

#### 思路

一次遍历，三路指针排序


``` js
var sortColors = function (nums) {
  let left = 0
  let current = 0
  let right = nums.length - 1
  while (current <= right) {
    if (nums[current] === 0) {
      swap(current, left)
      //left左侧一定全是0，left位置一定是1
      left++
      //left和current之间一定全是1
      current++
    } else if (nums[current] === 2) {
      swap(current, right)
      right--
      //这里不能current++了，因为right位置还未经过遍历，所以换过来的数字不确定
    } else {
      current++
    }
  }

  function swap(i, j) {
    let temp = nums[i]
    nums[i] = nums[j]
    nums[j] = temp
  }
};
```
