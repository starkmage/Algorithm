### 15.反转链表

---

输入一个链表，反转链表后，输出新链表的表头。

---

* 思路

创建一个新链表，遍历老链表，其实就是将遍历到的每一项插入到新链表的表头位置。

---

``` JS
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/


function ReverseList(pHead)
{
    // write code here
    let head;
 
    while(pHead !== null) {
        let val = pHead.val;
        let newNode = new ListNode(val);
        newNode.next = head;
        head = newNode;
        pHead = pHead.next;
    }
     
    return head;
}
```

---

使用这种方法要注意链表指针的修改顺序问题。

``` JS
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/


function ReverseList(pHead)
{
    // write code here
    let head;
    let p = pHead;
    let current = pHead;
    
    while(p !== null) {
        current = current.next;
        p.next = head;
        head = p;
        p = current;
    }
    
    return head;
}
```
