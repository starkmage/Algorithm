### 11.盛最多水的容器

---

给你 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

说明：你不能倾斜容器，且 n 的值至少为 2。

```
输入：[1,8,6,2,5,4,8,3,7]
输出：49
```

---

#### 思路

双指针法

基本的表达式: area = min(height[i], height[j]) * (j - i)

使用两个指针，值小的指针向内移动，这样就减小了搜索空间

因为面积取决于指针的距离与值小的值乘积，如果值大的值向内移动，距离一定减小，而求面积的另外一个乘数一定小于等于值小的值，因此面积一定减小

而我们要求最大的面积，因此值大的指针不动，而值小的指针向内移动遍历

``` js
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function(height) {
  let left = 0
  let right = height.length - 1
  let max = 0
  while (left < right) {
    let area 
    if (height[left] > height[right]) {
      area = (right - left) * height[right]
      right--
    } else {
      area = (right - left) * height[left]
      left++
    }
    if (area > max) {
      max = area
    }
  }
  return max
};
```
