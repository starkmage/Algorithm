### 148.排序链表

---

在 O(n log n) 时间复杂度和常数级空间复杂度下，对链表进行排序。

示例 1:
```
输入: 4->2->1->3
输出: 1->2->3->4
```
示例 2:
```
输入: -1->5->3->4->0
输出: -1->0->3->4->5
```
---

#### 思路

对链表进行排序，其实用到的就是归并排序，而且不需要开辟额外空间

注意新知识点，如何利用快慢指针找到链表的中点

``` js
var sortList = function(head) {
  if (head === null) return null
  return mergeSort(head)
};

function mergeSort(node) {
  if (node.next === null) return node
  //快慢指针找到链表中点
  let slow = node
  let fast = node
  let pre = null
  while (fast !== null && fast.next !== null) {
    pre = slow
    slow = slow.next
    fast = fast.next.next
  }
  pre.next = null
  let left = mergeSort(node)
  let right = mergeSort(slow)
  return merge(left, right)
}

function merge(left, right) {
  let res = new ListNode(0)
  let cur = res
  while (left !== null && right !== null) {
    if (left.val <= right.val) {
      cur.next = left
      cur = cur.next
      left = left.next
    } else {
      cur.next = right
      cur = cur.next
      right = right.next
    }
  }

  if (left !== null) cur.next = left
  if (right !== null) cur.next = right
  return res.next
}
```
