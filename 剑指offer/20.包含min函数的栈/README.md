### 20.包含min函数的栈

---

定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

注意：保证测试中不会当栈为空的时候，对栈调用pop()或者min()或者top()方法。

---

#### 思路

借助一个辅助栈，我们可以称为最小元素栈，每次压栈操作时, 如果压栈元素比当前最小元素更小, 就把这个元素压入最小元素栈, 原本的最小元素就成了次小元素。同理, 弹栈时, 如果弹出的元素和最小元素栈的栈顶元素相等, 就把最小元素的栈顶弹出。

``` JS
var MinStack = function() {
  this.stack = []
  this.minStack = [Infinity]
};

MinStack.prototype.push = function(x) {
  this.stack.push(x)
  this.minStack.push(Math.min(x, this.minStack[this.minStack.length - 1]))
};

MinStack.prototype.pop = function() {
  this.stack.pop()
  this.minStack.pop()
};

MinStack.prototype.top = function() {
  return this.stack[this.stack.length - 1]
};

MinStack.prototype.min = function() {
  return this.minStack[this.minStack.length - 1]
};
```
