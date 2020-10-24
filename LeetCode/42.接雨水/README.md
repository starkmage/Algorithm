### 42.接雨水

---

给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/rainwatertrap.png)

上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）

示例:
```
输入: [0,1,0,2,1,0,1,3,2,1,2,1]
输出: 6
```
---

#### 动态编程

找到 i 左右两侧最高的柱子，在这两个柱子中选一个矮的，减去 i 本身的高度，大于0的话就是 i 柱子存的水

``` js
var trap = function(height) {
  let len = height.length
  //这些情况不可能存水
  if (len === 0 || len === 1 || len === 2) return 0
  let leftMax = Array(len)
  leftMax[0] = height[0]
  let rightMax = Array(len)
  rightMax[len - 1] = height[len - 1]
  //一个柱子左侧最高值
  for (let i = 1; i < len; i++) {
    leftMax[i] = Math.max(leftMax[i - 1], height[i - 1])
  }
  //一个柱子右侧最高值
  for (let i = len - 2; i >= 0; i--) {
    rightMax[i] = Math.max(rightMax[i + 1], height[i + 1])
  }
  //每个柱子能存的最大水量
  let water = 0
  //开头和结尾不可能存水，直接跳过
  for (let i = 1; i < len - 1; i++) {
    let temp = Math.min(leftMax[i], rightMax[i])
    water += Math.max(0, temp - height[i])
  }
  return water
};
```

---

#### 双指针法

思想其实和上面的方法一样，只不过实现方式不一样

只需要遍历一次，而且需要存储临时数据的空间更小

``` js
var trap = function(height) {
  let len = height.length
  if (len === 0 || len === 1 || len === 2) return 0
  let left = 0
  let right = len - 1
  let leftMax = height[0]
  let rightMax = height[len - 1]
  let water = 0
  while(left < right) {
    leftMax = Math.max(leftMax, height[left])
    rightMax = Math.max(rightMax, height[right])
    if (leftMax < rightMax) {
      water += Math.max(0, leftMax - height[left])
      left++
    } else {
      water += Math.max(0, rightMax - height[right])
      right--
    }
  }
  return water
};
```
