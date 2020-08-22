### 23.合并K个升序链表

---

给你一个链表数组，每个链表都已经按升序排列。

请你将所有链表合并到一个升序链表中，返回合并后的链表。

示例 1：
```
输入：lists = [[1,4,5],[1,3,4],[2,6]]
输出：[1,1,2,3,4,4,5,6]
解释：链表数组如下：
[
  1->4->5,
  1->3->4,
  2->6
]
将它们合并到一个有序链表中得到。
1->1->2->3->4->4->5->6
```
示例 2：
```
输入：lists = []
输出：[]
```
示例 3：
```
输入：lists = [[]]
输出：[]
```
---

#### 思路

前面做过的第21题，合并两个升序的链表，这道题可以看做是那一道题的进阶版

用类似归并排序的方法，合并分治的思想，K个合并可以拆分成很多个两个合并，问题解决

``` js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode[]} lists
 * @return {ListNode}
 */
var mergeKLists = function(lists) {
  let len = lists.length
  if (len === 0) return null
  if (len === 1) return lists[0]
  let mid = Math.floor(len/2)
  let left = mergeKLists(lists.slice(0, mid))
  let right = mergeKLists(lists.slice(mid, len))
  return mergeTwoLists(left, right)
};

function mergeTwoLists(l1, l2) {
  if (l1 === null && l2 === null) return null
  if (l1 === null) return l2
  if (l2 === null) return l1
  let res = new ListNode(-1)
  let current = res
  while (l1 !== null && l2 !== null) {
    if (l1.val < l2.val) {
      current.next = l1
      l1 = l1.next
    } else {
      current.next = l2
      l2 = l2.next
    }
    current = current.next
  }
  current.next = l1 ? l1 : l2
  return res.next
}
```
