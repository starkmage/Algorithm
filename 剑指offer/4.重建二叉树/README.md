### 4.重建二叉树

---

输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

---

* 递归

``` JS
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */


function reConstructBinaryTree(pre, vin)
{
    // write code here
    if(pre.length === 0 || vin.length === 0) return null;
    let root = new TreeNode(pre[0]);
    
    let i = vin.indexOf(pre[0]);
    
    
    let tempPre1 = pre.slice(1, i + 1);
    let tempVin1 = vin.slice(0, i);

    let tempPre2 = pre.slice(i + 1);
    let tempVin2 = vin.slice(i + 1);
    
    root.left = reConstructBinaryTree(tempPre1, tempVin1);
    root.right = reConstructBinaryTree(tempPre2, tempVin2);
    
    return root;
}
```
