### 14.链表中倒数第k个结点

---

输入一个链表，输出该链表中倒数第k个结点。

---

* 常规思路，两次遍历

``` JS
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/


function FindKthToTail(head, k)
{
    // write code here
    if(head === null) return null;
    let length = 1;
    let current = head;
    while(current.next !== null) {
        current = current.next;
        length++;
    }
    if(k > 0 && k <= length) {
        let index = 1;
        let res = head;
        while(index < length - k + 1) {
            res = res.next;
            index++;
        }
        return res;
    } else {
        return null;
    }
}
```

---

* 快慢指针，一次遍历

``` JS
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/


function FindKthToTail(head, k)
{
    // write code here
    if(head === null || k <= 0) return null;
    let length = 1;
    let current = head;
    let res = null;
    while(current !== null) {
        current = current.next;
        if(length >= k) {
            if(res === null) {
                res = head;
            } else {
                res = res.next;
            }
        }
        length++;
    }
    return res;
}
```
