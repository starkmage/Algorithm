### 160.相交链表

---

编写一个程序，找到两个单链表相交的起始节点，没有输出null

---

#### 思路

和“剑指offer-36.两个链表的第一个公共节点”一模一样

假定 List1 长度: a+n，List2 长度:b+n, 且 a<b，那么 p1 会先到链表尾部, 这时 p2 走到 a+n 位置,将 p1 换成 List2 头部，接着 p2 再走 b+n-(n+a) =b-a 步到链表尾部,这时 p1 也走到 List2 的 b-a 位置，还差 a 步就到可能的第一个公共节点。将 p2 换成 List1 头部，p2 走 a 步也到可能的第一个公共节点。 如果恰好 p1==p2 ,那么 p1 就是第一个公共节点。或者 p1 和 p2 一起走 n 步到达列表尾部 null ，二者没有公共节点，退出循环。时间复杂度为O(n)。

``` js
var getIntersectionNode = function(headA, headB) {
  if (headA === null || headB === null) return null
  let a = headA
  let b = headB
  while (a !== b) {
    a === null ? a = headB : a = a.next
    b === null ? b = headA : b = b.next
  }
  return a
};
```
