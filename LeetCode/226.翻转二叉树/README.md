### 226.翻转二叉树

---

翻转一棵二叉树。

示例：
```
输入：

     4
   /   \
  2     7
 / \   / \
1   3 6   9
输出：

     4
   /   \
  7     2
 / \   / \
9   6 3   1
```
---

#### 递归

这道题和“剑指offer-18.二叉树的镜像”一样

和“LeetCode-101.对称二叉树”很相似

``` js
var invertTree = function(root) {
  if (root === null) return null

  let temp = root.left
  root.left = root.right
  root.right = temp

  invertTree(root.left)
  invertTree(root.right)

  return root
};
```
