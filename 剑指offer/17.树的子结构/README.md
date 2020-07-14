### 17.树的子结构

---

输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）。

---

* 思路

递归，下面两种完全一致，只不过第二种利用短路，代码更简洁。

---

``` JS
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */


function HasSubtree(pRoot1, pRoot2)
{
    // write code here
    let result = false;
    if(pRoot1 !== null && pRoot2 !== null) {
        if(pRoot1.val === pRoot2.val) {
            result = SameTree(pRoot1, pRoot2);
        }
        if(!result) {
            result = HasSubtree(pRoot1.left, pRoot2);
        }
        if(!result) {
            result = HasSubtree(pRoot1.right, pRoot2);
        }
    }
    return result;
}

 
function SameTree(node1, node2) {
    //注意，是子结构，不一定是子树，所以node2为空时，node1可以不为空
    if(node2 === null) return true;
    if(node1 === null) return false;
    if(node1.val !== node2.val) {
        return false;
    } else {
        return SameTree(node1.left, node2.left) && SameTree(node1.right, node2.right)
    }
}
```

---

``` JS
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */


function HasSubtree(pRoot1, pRoot2)
{
    // write code here
    if(pRoot1 === null || pRoot2 === null) return false;
    
    return SameTree(pRoot1, pRoot2) || HasSubtree(pRoot1.left, pRoot2) || HasSubtree(pRoot1.right, pRoot2);
}


function SameTree(node1, node2) {
    //注意，是子结构，不一定是子树，所以node2为空时，node1可以不为空
    if(node2 === null) return true;
    if(node1 === null) return false;
    if(node1.val !== node2.val) {
        return false;
    } else {
        return SameTree(node1.left, node2.left) && SameTree(node1.right, node2.right)
    }
}
```
