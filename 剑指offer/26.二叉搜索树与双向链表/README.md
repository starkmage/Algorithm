### 26.二叉搜索树与双向链表

---

输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。

---

* 思路

看到按大小排序首先想到了中序遍历，题目要求不能创建任何新的节点，在`ConvertHelp`里，借助`pre`标记链表中的上一个节点。

``` js
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */

function Convert(pRootOfTree)
{
    // write code here
    if (pRootOfTree === null) return null
    ConvertHelp(pRootOfTree, null)
    //回到链表起点
    while (pRootOfTree.left !== null) {
        pRootOfTree = pRootOfTree.left
    }
    return pRootOfTree
}

function ConvertHelp(current, pre) {
    if (current.left) {
        pre = ConvertHelp(current.left, pre)
    }
    
    current.left = pre
    if(pre) pre.right = current
    pre = current
    
    if (current.right) {
        pre = ConvertHelp(current.right, pre)
    }
    
    return pre
}
```
