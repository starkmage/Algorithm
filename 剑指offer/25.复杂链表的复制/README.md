### 25.复杂链表的复制

---

输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针random指向一个随机节点），请对此链表进行深拷贝，并返回拷贝后的头结点。（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空）。

---

* 思路

主要分成两步：

1.依次复制旧链表的每个节点，同时把新节点插入到旧节点的后面。

2.对每个新节点的`random`指针赋值，同时把新节点从旧链表中抽出来，得到我们想要的新链表。

---

``` JS
/*function RandomListNode(x){
    this.label = x;
    this.next = null;
    this.random = null;
}*/


function Clone(pHead)
{
    // write code here
    if(pHead === null) return null;
    let pre = pHead;
    let current = pHead.next;
    while(current !== null) {
        let newNode = new RandomListNode(pre.label);
        pre.next = newNode;
        newNode.next = current;
        pre = current;
        current = current.next;
    }
    //复制最后一个节点
    let newNode = new RandomListNode(pre.label);
    pre.next = newNode;
    
    let pre2 = pHead;
    let current2 = pHead.next;
    let head = current2;
    
    while(pre2 !== null) {
        if(pre2.random !== null) {
            current2.random = pre2.random.next;
        }
        pre2 = current2.next;
        if(pre2 !== null) {
            current2.next = pre2.next;
        }
        current2 = current2.next;
    }
    
    return head;
}
