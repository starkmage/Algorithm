### 142.环形链表II

---

给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

---

#### 思路

和“剑指offer-55.链表中环的入口结点”一模一样

``` js
var detectCycle = function(head) {
  if (head === null || head.next === null) return null
  let fast = head
  let slow = head
  while (fast && fast.next !== null) {
    fast = fast.next.next
    slow = slow.next
    if (fast === slow) break
  }
  if (fast === null || fast.next === null) return null
  slow = head
  while (fast !== slow) {
    fast = fast.next
    slow = slow.next
  }
  return slow
};
```
