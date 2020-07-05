### 57.二叉树的下一个节点

---

给定一个二叉树和其中的一个结点，请找出中序遍历顺序的下一个结点并且返回。注意，树中的结点不仅包含左右子结点，同时包含指向父结点的指针。

---

* 思路

分3种情况考虑：

1. pNode为空节点；

2. pNode有右子节点；
找到pNode右子树中最左的节点即可。

3. pNode没有右节点。
这种情况最复杂，如果该节点是其父节点的左孩子，则返回其父节点；否则继续向上遍历其父节点的父节点，直到找到第一个为左孩子的，返回这个左孩子的父节点，或者，直到pNode到达根节点，返回`null`。

---

``` JS
/*function TreeLinkNode(x){
    this.val = x;
    this.left = null;
    this.right = null;
    this.next = null;
}*/


function GetNext(pNode)
{
    // write code here
    
    //1.pNode为空节点
    if(pNode === null) {
        return null;
    }
    
    //2.pNode有右子节点
    if(pNode.right !== null) {
        pNode = pNode.right;
        while(pNode.left !== null) {
            pNode = pNode.left;
        }
        return pNode;
    } else {    //3.pNode没有右节点
        //while条件注意顺序，需要先判断pNode是不是到达根节点了，如果到了，则pNode.next.left会报错
        while(pNode.next !== null && pNode !== pNode.next.left) {
            pNode = pNode.next;
        }
        return pNode.next;
    }
}
```
