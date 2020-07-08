### 58.对称的二叉树

---

请实现一个函数，用来判断一棵二叉树是不是对称的。注意，如果一个二叉树同此二叉树的镜像是同样的，定义其为对称的。

---

* 递归

``` JS
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */


function isSymmetrical(pRoot)
{
    // write code here
    if(pRoot === null) return true;
    return isSymmrtricalHelp(pRoot.left, pRoot.right);
}


function isSymmrtricalHelp(left, right) {
    if(left === null && right === null) return true;
    if(left === null || right === null) return false;
    return left.val === right.val && isSymmrtricalHelp(left.left, right.right) && isSymmrtricalHelp(left.right, right.left);
}
```
