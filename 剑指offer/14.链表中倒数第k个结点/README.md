### 14.链表中倒数第k个结点

---

输入一个链表，输出该链表中倒数第k个结点。

---

#### 快慢指针，一次遍历

``` JS
var getKthFromEnd = function(head, k) {
  if (head === null) return null
  let first = head, second = head
  for (let i = 0; i < k; i++) {
    first = first.next
  }
  if (first === null) return head
  while (first.next) {
    first = first.next
    second = second.next
  }
  return second.next
};
```
