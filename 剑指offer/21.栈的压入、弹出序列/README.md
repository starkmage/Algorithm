### 21.栈的压入、弹出序列

---

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）

---

* 思路

借助一个辅助栈，从左到右扫描出栈序列，每次压栈后将满足出栈条件的元素出栈，最后判断辅助栈是否为空，空说明所有元素都成功出栈，否则有元素未成功出栈，出栈序列错误。

---

``` JS
function IsPopOrder(pushV, popV)
{
    // write code here
    if(pushV.length === 0 || popV.length === 0) return false;
    let stack = [];
    //对popV遍历
    for(let i = 0; i < popV.length; i++) {
        //在找到与popV[i]相同的之前，把pushV元素从前压入stack
        while(pushV.length > 0 && popV[i] !== pushV[0]) {
            stack.push(pushV.shift());
        }
        //1.popV[i]和即将要入栈的元素相等
        if(pushV.length > 0 && popV[i] === pushV[0]) {
            pushV.shift();
        }
        //2.popV[i]和刚刚入栈的元素相等
        if(stack.length > 0 && popV[i] === stack[stack.length-1]) {
            stack.pop();
        }
    }
    return stack.length === 0;
}
```
