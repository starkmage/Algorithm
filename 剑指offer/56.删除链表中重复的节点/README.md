### 56.删除链表中重复的节点

---

在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。 例如，链表1->2->3->3->4->4->5 处理后为 1->2->5。

---

* 思路

这道题最关键的地方就是构造一个头节点，可以避免很多复杂的情况。

---

``` JS
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/


function deleteDuplication(pHead)
{
    // write code here
    if(pHead === null || pHead.next === null) return pHead;
    //最巧妙的地方，构造一个头节点
    let head = new ListNode(0);
    head.next = pHead;
    let pre = head;
    let current = head.next;
    
    while(current !== null) {
        if(current.next !== null && current.val === current.next.val) {
            while(current.next !== null && current.val === current.next.val) {
                current = current.next;
            }
            current = current.next;
            pre.next = current;
        } else {
            pre = current;
            current = current.next;
        }
    }
    
    return head.next;
}
```
