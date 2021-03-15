### 26.二叉搜索树与双向链表

---

输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。

---

* 思路

看到按大小排序首先想到了中序遍历，题目要求不能创建任何新的节点，在`ConvertHelp`里，借助`pre`标记链表中的上一个节点。和LeetCode中114题很像，稍微多了一步而已。

``` js
function Convert(pRootOfTree)
{
    // write code here
  let last = null
  function reverseTree(node) {
    if (node === null) return
    reverseTree(node.right)
    node.right = last
    last = node
    reverseTree(node.left)
  }
  reverseTree(pRootOfTree)
  let cur = last, pre = null
  while (cur) {
    cur.left = pre
    pre = cur
    cur = cur.right
  }
  return last
}
```
