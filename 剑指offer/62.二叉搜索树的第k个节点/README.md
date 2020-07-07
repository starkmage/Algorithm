### 62.二叉搜索树的第k个节点

---

给定一棵二叉搜索树，请找出其中的第k小的结点。例如， （5，3，7，2，4，6，8）    中，按结点数值大小顺序第三小结点的值为4。

---

* 思路

二叉搜索树的中序遍历得到的结果就是从小到大排列的，可以利用这一点。

``` JS
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */


function KthNode(pRoot, k)
{
    // write code here
    if(k <= 0) return null;
    let array = [];
    inOrderTraverse(pRoot, array);
    return array[k-1];
}


function inOrderTraverse(root, array) {
    if(root === null) return;
    
    inOrderTraverse(root.left, array);
    array.push(root);
    inOrderTraverse(root.right, array);
}
