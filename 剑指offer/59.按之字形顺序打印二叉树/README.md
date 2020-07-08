### 59.按之字形顺序打印二叉树

---

请实现一个函数按照之字形打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右至左的顺序打印，第三行按照从左到右的顺序打印，其他行以此类推。

---

* 思路

这个其实和分层打印一样，只不过不同的是需要调整队列中部分数组元素内的元素顺序。

---

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
    for(let i = 0; i < queue.length; i++) {
        if(i % 2 === 1) {
            queue[i].reverse();
        }
    }
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
