### 101.对称二叉树

---

给定一个二叉树，检查它是否是镜像对称的。
 
```
例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

    1
   / \
  2   2
 / \ / \
3  4 4  3
 
但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

    1
   / \
  2   2
   \   \
   3    3
```
进阶：

你可以运用递归和迭代两种方法解决这个问题吗？
---

#### 递归

和“剑指offer-58.对称的二叉树”一模一样

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
 * @return {boolean}
 */
var isSymmetric = function(root) {
  if (root === null) return true
  return help(root.left, root.right)
};

function help(left, right) {
  if (left === null && right === null) return true
  if (left === null || right === null) return false
  return left.val === right.val && help(left.left, right.right) && help(left.right, right.left)
}
```

---

#### 迭代

``` js
var isSymmetric = function(root) {
  if (root === null) return true
  const stack = [root.left, root.right]
  while (stack.length) {
    let r = stack.pop()
    let l = stack.pop()
    if (l === null && r === null) continue
    if (l && r && l.val === r.val) {
      stack.push(l.left, r.right, l.right, r.left)
    } else {
      return false
    }
  }
  return true
}
```
};
