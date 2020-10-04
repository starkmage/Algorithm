### 46.孩子们的游戏

---
0,1,,n-1这n个数字排成一个圆圈，从数字0开始，每次从这个圆圈里删除第m个数字。求出这个圆圈里剩下的最后一个数字。

例如，0、1、2、3、4这5个数字组成一个圆圈，从数字0开始每次删除第3个数字，则删除的前4个数字依次是2、0、4、1，因此最后剩下的数字是3。

示例 1：
```
输入: n = 5, m = 3
输出: 3
```
示例 2：
```
输入: n = 10, m = 17
输出: 2
```
---

#### 队列思路

利用队列，先将所有小朋友压入队列，报完数的小朋友从队列出来，压入队尾，依次循环，而报数为m - 1的小朋友出队后不再进入队列，最终剩下的小朋友获胜。

---

``` JS
var lastRemaining = function(n, m) {
  let queue = Array(n).fill(0).map((val, index) => index)
  while (queue.length > 1) {
    for (let i = 1; i < m; i++) queue.push(queue.shift())
    queue.shift()
  }
  return queue[0]
};
```

#### 公式法

上述思路时间复杂度为 `O(nm)` ，在数据非常大的时候，会超出时间限制，[参考这里](https://blog.csdn.net/u011500062/article/details/72855826)

``` js
var lastRemaining = function(n, m) {
  let res = 0
  for (let i = 2; i <= n; i++) {
    res = (res + m) % i
  }
  return res
};
```
