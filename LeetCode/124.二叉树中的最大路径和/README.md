### 124.二叉树中的最大路径和

---

给定一个非空二叉树，返回其最大路径和。

本题中，路径被定义为一条从树中任意节点出发，沿父节点-子节点连接，达到任意节点的序列。该路径至少包含一个节点，且不一定经过根节点。

示例 1：
```
输入：[1,2,3]

       1
      / \
     2   3

输出：6
```
示例 2：
```
输入：[-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

输出：42
```
---

#### 思路

二叉树问题当然是递归，可以和“剑指offer-24.二叉树中和为某一值的路径”结合看看

``` js
var maxPathSum = function(root) {
  let res = -Infinity
  help(root)
  return res

  function help(node) {
    if (node === null) return 0
    //求 node 左子树的路径最大和，如果小于 0，则取 0，代表不会走这个子树
    let left = Math.max(0, help(node.left))
    let right = Math.max(0, help(node.right))
    //要判断 res 和 以 node 为根节点的树的路径和谁更大 
    res = Math.max(res, node.val + left + right)
    //向 node 的父节点迭代，选择 node.val + 较大的那条子树
    return node.val + Math.max(left, right)
  }
};
```
