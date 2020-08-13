### 55.链表中环的入口结点

---

给一个链表，若其中包含环，请找出该链表的环的入口结点，否则，输出null。

---

* 思路

1. 设置快慢指针，慢指针slow一次走一步，快指针fast一次走两步，如果有环，快慢指针一定在环中某点相遇

2. 因为slow一旦进环，可看作fast在后面追赶slow的过程，每次两者都接近一步，最后一定能追上

3. 两个指针分别从链表头和相遇点继续出发，每次走一步，最后一定相遇与环入口

4. 证明3

    * 链表头到环入口长度为--a，环入口到相遇点长度为--b，相遇点到环入口长度为--c

    * 相遇时快指针路程=a+(b+c)k+b ，k>=1  其中b+c为环的长度，k为绕环的圈数（k>=1,即最少一圈，不能是0圈，不然和慢指针走的一样长，矛盾），慢指针路程=a+b

    * 快指针走的路程是慢指针的两倍，所以：（a+b）*2=a+(b+c)k+b，化简可得：a=(k-1)(b+c)+c
    
    * 这个式子的意思是： 链表头到环入口的距离=相遇点到环入口的距离+（k-1）圈环长度。其中k>=1,所以k-1>=0圈。所以两个指针分别从链表头和相遇点出发，最后一定相遇于环入口。
    
``` js
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function EntryNodeOfLoop(pHead)
{
    // write code here
  if (pHead === null || pHead.next === null) return null
  let slow = pHead
  let fast = pHead
  while (fast.next !== null) {
    slow = slow.next
    fast = fast.next.next
    if (slow === fast) break
  }
  if (fast.next === null) return null
  slow = pHead
  while (slow !== fast) {
    slow = slow.next
    fast = fast.next
  }
  return slow
}
```
