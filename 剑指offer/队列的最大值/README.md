### 队列的最大值

请定义一个队列并实现函数 max_value 得到队列里的最大值，要求函数max_value、push_back 和 pop_front 的均摊时间复杂度都是O(1)。

若队列为空，pop_front 和 max_value 需要返回 -1

示例 1：
```
输入: 
["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
[[],[1],[2],[],[],[]]
输出: [null,null,null,2,1,2]
```
示例 2：
```
输入: 
["MaxQueue","pop_front","max_value"]
[[],[],[]]
输出: [null,-1,-1]
```
---

#### 思路

和“包含min函数的栈”非常相似，但是因为队列先进先出的特点，在处理最大值的时候，有一些不同

``` js
var MaxQueue = function() {
  this.queue = []
  this.maxQueue = []
};

MaxQueue.prototype.max_value = function() {
  if (this.queue.length === 0) return -1
  return this.maxQueue[0]
};


MaxQueue.prototype.push_back = function(value) {
  this.queue.push(value)
  while (this.maxQueue.length && value > this.maxQueue[this.maxQueue.length - 1]) {
    this.maxQueue.pop()
  }
  this.maxQueue.push(value)
};

MaxQueue.prototype.pop_front = function() {
  if (this.queue.length === 0) return -1
  let res = this.queue.shift()
  if (res === this.maxQueue[0]) this.maxQueue.shift()
  return res
};
```
