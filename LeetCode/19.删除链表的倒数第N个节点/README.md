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

删除的时候，注意区分3种情况，并且要注意3种情况的先后顺序，否则会出现一些特殊情况的错误，比如只有1个节点的时候

``` js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} n
 * @return {ListNode}
 */
var removeNthFromEnd = function(head, n) {
  if (head === null) return null
  let first = head
  let second = head
  let pre = null
  let count = 1
  while (first.next !== null) {
    first = first.next
    if (count >= n) {
      pre = second
      second = second.next
    }
    count++
  }
  if (n === count) {
    head = head.next
  } else if (n === 1) {
    pre.next = null
  } else {
    pre.next = second.next
  }
  return head
};
```
