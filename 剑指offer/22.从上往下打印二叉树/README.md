### 22.从上往下打印二叉树

---

从上往下打印出二叉树的每个节点，同层节点从左至右打印。

---

* 思路

这和第60题完全一样，按层次遍历二叉树。

---

* 递归

``` JS
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */


function PrintFromTopToBottom(root)
{
    // write code here
    let array = [];
    depthTraverse(root, 1, array);
    return array;
}


function depthTraverse(root, depth, array) {
    if(root === null) return;
    if(depth > array.length) {
        array.push([]);
    }
    
    array[depth-1].push(root.val);
    depthTraverse(root.left, depth+1, array);
    depthTraverse(root.right, depth+1, array);
}
```
