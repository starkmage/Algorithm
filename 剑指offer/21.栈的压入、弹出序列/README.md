### 21.栈的压入、弹出序列

---

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）

---

* 思路

借助一个辅助栈，从左到右扫描出栈序列，每次压栈后将满足出栈条件的元素出栈，最后判断辅助栈是否为空，空说明所有元素都成功出栈，否则有元素未成功出栈，出栈序列错误。

---

``` JS
var validateStackSequences = function(pushed, popped) {
  if (pushed.length !== popped.length) return false
  const stack = []
  while (pushed.length) {
    stack.push(pushed.shift())
    while (stack.length && stack[stack.length - 1] === popped[0]) {
      stack.pop()
      popped.shift()
    }
  }
  return stack.length === 0
};
```
