### 19.删除链表的倒数第N个节点

---

给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：

给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
说明：

给定的 n 保证是有效的。

进阶：

你能尝试使用一趟扫描实现吗？

---

#### 思路

这道题其实和剑指offer第14题很类似

设置两个指针，第一个指针先走N步，当第一个指针遍历到头时，第二个指针的位置就是倒数第N个节点

``` js
var removeNthFromEnd = function(head, n) {
  if (head === null) return null
  let first = head, second = head
  for (let i = 0; i < n; i++) {
    first = first.next
  }
  // 删除第一个节点的情况
  if (first === null) return head.next
  // 判断条件很重要
  while (first.next) {
    first = first.next
    second = second.next
  }
  second.next = second.next.next
  return head
};
```
