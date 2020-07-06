### 16.合并两个排序的链表

---

输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。

---

* 递归

``` JS
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/


function Merge(pHead1, pHead2)
{
    // write code here
    if(pHead1 === null) {
        return pHead2;
    }
    if(pHead2 === null) {
        return pHead1;
    }
    
    let res;
    
    if(pHead1.val < pHead2.val) {
        res = pHead1;
        res.next = Merge(pHead1.next, pHead2);
    } else {
        res = pHead2;
        res.next = Merge(pHead1, pHead2.next)
    }
    return res;
}
```

---

* 非递归

``` JS
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/


function Merge(pHead1, pHead2)
{
    // write code here
    if(pHead1 === null) {
        return pHead2;
    }
    if(pHead2 === null) {
        return pHead1;
    }
    
    let res = new ListNode(0);
    res.next = null;
    let root = res;
    
    while(pHead1 !== null && pHead2 !== null) {
        if (pHead1.val < pHead2.val) {
            res.next = pHead1;
            res = pHead1;
            pHead1 = pHead1.next;
        } else {
            res.next = pHead2;
            res = pHead2;
            pHead2 = pHead2.next;
        }
    }
    
    if(pHead1 !== null) {
        res.next = pHead1;
    } 
    if(pHead2 !== null) {
        res.next = pHead2;
    }
    
    return root.next;
}
```
