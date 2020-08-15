### 2.两数相加

---

给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

```
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
```

---

#### 思路

* 猛一看好像个位数在前不方便，但是在链表中，其实这样更方便，直接两个链表的值依次相加即可

* 需要注意的点有以下几点

  1. 满10进1，在下一轮加上up了后，up不要忘记归0
  
  2. 不要忘记最后剩一个up的情况
  
  3. sum大于等于10时，不应该去sum%10，此时sum等于10时，是1，而不是0
  
``` js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
  let head = new ListNode(0)
  let l = head
  let up = 0
  let sum = 0
  while(l1 !== null && l2 !== null) {
    sum = l1.val + l2.val + up
    //重置up
    up = 0
    if (sum >= 10) {
      up = 1
      sum = sum - 10
    }
    l.next = new ListNode(sum)
    l = l.next
    l1 = l1.next
    l2 = l2.next
  }
  while (l1 !== null) {
    sum = l1.val + up
    up = 0
    if (sum >= 10) {
      up = 1
      sum = sum - 10
    }
    l.next = new ListNode(sum)
    l = l.next
    l1 = l1.next
  }
  while (l2 !== null) {
    sum = l2.val + up
    up = 0
    if (sum >= 10) {
      up = 1
      sum = sum - 10
    }
    l.next = new ListNode(sum)
    l = l.next
    l2 = l2.next
  }
  if (up) {
    l.next = new ListNode(up)
  }
  return head.next
};
```

* 进行了一些精简，思想完全一样

``` js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
  let head = new ListNode(0)
  let l = head
  let up = 0
  let sum = 0
  while(l1 !== null || l2 !== null) {
    sum = (l1 ? l1.val : 0) + (l2 ? l2.val : 0) + up
    //重置up
    up = 0
    if (sum >= 10) {
      up = 1
      sum = sum - 10
    }
    l.next = new ListNode(sum)
    l = l.next
    if (l1) l1 = l1.next
    if (l2) l2 = l2.next
  }
  if (up) {
    l.next = new ListNode(up)
  }
  return head.next
};
```
