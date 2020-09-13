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
  if (head === null || head.next === null) return true
  let fast = head
  let slow = head
  // 1. 快慢指针找到链表的中点，是靠后的那个中点
  while (fast) {
    fast = fast.next ? fast.next.next : fast.next
    slow = slow.next
  }
  // 2. 反转后半部分链表
  let cur = slow
  let head1 = null
  while (slow) {
    slow = slow.next
    cur.next = head1
    head1 = cur
    cur = slow
  }
  // 3. 判断是否相等
  while (head1) {
    if (head.val !== head1.val) return false
    head = head.next
    head1 = head1.next
  }

  return true
};
```
