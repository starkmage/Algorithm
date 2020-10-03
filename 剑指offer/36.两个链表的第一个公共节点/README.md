### 36.两个链表的第一个公共节点

---

输入两个链表，找出它们的第一个公共结点。

---

* 思路

假定 List1 长度: a+n，List2 长度:b+n, 且 a<b，那么 p1 会先到链表尾部, 这时 p2 走到 a+n 位置,将 p1 换成 List2 头部，接着 p2 再走 b+n-(n+a) =b-a 步到链表尾部,这时 p1 也走到 List2 的 b-a 位置，还差 a 步就到可能的第一个公共节点。将 p2 换成 List1 头部，p2 走 a 步也到可能的第一个公共节点。
如果恰好 p1==p2 ,那么 p1 就是第一个公共节点。或者 p1 和 p2 一起走 n 步到达列表尾部 null ，二者没有公共节点，退出循环。时间复杂度为`O(n)`。

``` JS
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/

function FindFirstCommonNode(pHead1, pHead2)
{
    // write code here
    let p1 = pHead1;
    let p2 = pHead2;
    
    while(p1 !== p2) {
        p1 === null ? p1 = pHead2 : p1 = p1.next;
        p2 === null ? p2 = pHead1 : p2 = p2.next;
    }
    
    return p1;
}
```
