### 14.环形链表

---

给定一个链表，判断链表中是否有环。

---

#### 思路

这道题是“剑指offer-55.链表中环的入口结点”的简化版

设置快慢指针，如果有环，它们必然相遇

``` js
var hasCycle = function(head) {
 if (head === null || head.next === null) return false
 let fast = head
 let slow = head
 while(fast && fast.next !== null) {
   fast = fast.next.next
   slow = slow.next
   if (fast === slow) return true
 }
 return false
};
```
