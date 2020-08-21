### 21.合并两个有序链表

---

将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

示例：
```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```
---

#### 思路

类似归并排序的合并过程

注意最后剩下哪个，就把哪个直接拼在后面

``` js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var mergeTwoLists = function(l1, l2) {
    if (l1 === null && l2 === null) return null
    if (l1 === null) return l2
    if (l2 === null) return l1
    let res = new ListNode(-1)
    let current = res
    while (l1 !== null && l2 !== null) {
      if  (l1.val < l2.val) {
        current.next = l1
        l1 = l1.next
      } else {
        current.next = l2
        l2 = l2.next
      }
      current = current.next
    }
    if (l1 !== null) {
      current.next = l1
    }
    if (l2 !== null) {
      current.next = l2
    }
    return res.next
};
```
