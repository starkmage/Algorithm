### 5.用两个栈实现队列

---

用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

---

* 思路

栈1：
负责入队列存储

栈2：
出队列时将栈1的数据依次出栈，并入栈到栈2中，栈2出栈即栈1的底部数据即队列要出的数据。

关键点：
**栈2为空才能补充栈1的数据，否则会打乱当前的顺序。**

``` js
let inStack = [];
let outStack = [];

function push(node)
{
    // write code here
    inStack.push(node);
}
function pop()
{
    // write code here
    if (!outStack.length) {
        while(inStack.length) {
            outStack.push(inStack.pop())
        }
    }
    return outStack.pop();
}
```
