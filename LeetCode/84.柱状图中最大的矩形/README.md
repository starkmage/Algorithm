### 84.柱形图中最大的矩形

---

给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/histogram.png)

以上是柱状图的示例，其中每个柱子的宽度为 1，给定的高度为 [2,1,5,6,2,3]。

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/histogram_area.png)
 
图中阴影部分为所能勾勒出的最大矩形面积，其面积为 10 个单位。

示例:
```
输入: [2,1,5,6,2,3]
输出: 10
```
---

#### 单调栈

这道题思路很不好想，贴一个[大佬的链接](https://blog.csdn.net/Zolewit/article/details/88863970)，可详细参考

说一下需要注意的地方，基于各个高度的最大矩形是在出栈的时候计算的，因此必须要让所有高度都出栈，所以要在原始数组后添一个0，这样才能最终让栈清空

``` js
/**
 * @param {number[]} heights
 * @return {number}
 */
var largestRectangleArea = function(heights) {
  if (heights.length === 0) return 0
  heights.push(0)
  //单调递增栈
  //栈里维护的是下标值，不是柱子高度
  let stack = []
  let max = 0
  for (let i = 0; i < heights.length; i++) {
    //当 i 比栈顶柱子矮，栈顶柱子下标出栈，找到左侧第一个比 i 矮的柱子
    while (stack.length && heights[i] < heights[stack[stack.length - 1]]) {
      // i 是右侧第一个比 index 矮的柱子
      let index = stack.pop()
      //当栈为空，证明栈内所有柱子都比 i 高，而此时 index 又是 i 左侧最矮的柱子，所以以heights[index]为高的最大矩形长为 i
      if (stack.length === 0) {
        max = Math.max(max, heights[index] * i)
      }
      // index 弹出了，此时栈顶柱子比 index 矮，而 i 是右侧第一个矮于 index 的柱子，
      // 这里为什么减 1，因为 i 比 index 矮， 栈顶也比 index 矮，比如 index 为 3，而栈顶为 2，i 为5，实际长度为 2
      else {
        max = Math.max(max, heights[index] * (i - stack[stack.length - 1] - 1))
      }
    }
    stack.push(i)
  }
  return max
};
```
