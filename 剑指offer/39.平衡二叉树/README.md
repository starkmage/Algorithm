### 39 平衡二叉树

---

输入一棵二叉树，判断该二叉树是否是平衡二叉树。

在这里，我们只需要考虑其平衡性，不需要考虑其是不是排序二叉树。

---

* 思路

从下往上遍历，如果子树是平衡二叉树，则返回子树的高度；如果发现子树不是平衡二叉树，则直接停止遍历，这样至多只对每个结点访问一次。

---

* 剪枝方法

``` JS
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */


function IsBalanced_Solution(pRoot)
{
    // write code here
    return getDepth(pRoot) !== -1;
}


function getDepth(root) {
    
    if(root === null) return 0;
    
    let left = getDepth(root.left);
    if(left === -1) return -1;
    let right = getDepth(root.right);
    if(right === -1) return -1;
    
    return Math.abs(left - right) > 1 ? -1 : 1 + Math.max(left, right);
}
```
