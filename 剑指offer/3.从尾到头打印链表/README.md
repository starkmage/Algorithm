### 3.从尾到头打印链表

---

输入一个链表，按链表从尾到头的顺序返回一个ArrayList。

---

* 思路

这个题利用JS中的`unshift`方法可以简洁的实现，注意题中要求输出的是链表的值。

``` JS
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/


function printListFromTailToHead(head)
{
    // write code here
    let array = [];
    while(head !== null) {
        array.unshift(head.val);
        head = head.next;
    }
    return array;
}
```
