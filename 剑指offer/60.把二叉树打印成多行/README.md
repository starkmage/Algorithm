### 60.把二叉树打印成多行

---

从上到下按层打印二叉树，同一层结点从左至右输出。每一层输出一行。

---

* 思路

首先想到二叉树的先序遍历，结合多维数组 queue ，每一层的二叉树节点数据存到一个数组中，比如第1层的二叉树节点数据存到 queue[0] 里，第2层的二叉树节点数据存到 queue[1] 里，利用 depth 标记层数，参考先序遍历的过程进行递归，个人感觉最难想到的地方是 depth + 1 这个参数的设置。

---

* 二叉树递归

``` JS
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */


function Print(pRoot)
{
    // write code here
    let queue = [];
    preTraverse(pRoot, 1, queue);
    return queue;
}


function preTraverse(key, depth, queue) {
    if(key === null) return;
    
    if(queue.length < depth) {
        queue.push([]);
    }
    queue[depth - 1].push(key.val);
    preTraverse(key.left, depth + 1, queue);
    preTraverse(key.right, depth + 1, queue);
}
```
