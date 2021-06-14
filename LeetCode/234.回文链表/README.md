### 234.回文链表

---

请判断一个链表是否为回文链表。

示例 1:
```
输入: 1->2
输出: false
```
示例 2:
```
输入: 1->2->2->1
输出: true
```
进阶：
你能否用 O(n) 时间复杂度和 O(1) 空间复杂度解决此题？

---

#### 思路

这个题考查的非常综合

1. 快慢指针找链表中点

2. 链表的反转

``` js
var isPalindrome = function(head) {
  if (!head || !head.next) return true
  let fast = head, slow = head, pre = null
  while (fast && fast.next) {
    fast = fast.next.next
    pre = slow
    slow = slow.next
  }
  pre.next = null
  let l2 = null, temp
  while (slow) {
    temp = slow.next
    slow.next = l2
    l2 = slow
    slow = temp
  }
  let l1 = head
  // l1必然不长于l2
  while (l1 && l2) {
    if (l1.val !== l2.val) return false
    l1 = l1.next
    l2 = l2.next
  }
  return true
};
```
