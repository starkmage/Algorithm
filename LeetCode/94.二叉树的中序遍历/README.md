### 94.二叉树的中序遍历

---

给定一个二叉树，返回它的中序 遍历。

示例:
```
输入: [1,null,2,3]
   1
    \
     2
    /
   3

输出: [1,3,2]
```

进阶: 递归算法很简单，你可以通过迭代算法完成吗？

---

#### 递归算法

``` js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var inorderTraversal = function (root) {
  var res = []
  midTraverse(root)
  function midTraverse(node) {
    if (node === null) return
    midTraverse(node.left)
    res.push(node.val)
    midTraverse(node.right)
  }
  return res
};
```

#### 迭代算法

``` js
var inorderTraversal = function(root) {
  let res = []
  let stack = []
  let node = root
  while (node || stack.length) {
    if (node) {
      stack.push(node)
      node = node.left
    } else {
      node = stack.pop()
      res.push(node.val)
      node = node.right
    }
  }
  return res
};
```
