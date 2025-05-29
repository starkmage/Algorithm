### 128.最长连续序列

---

给你一个二叉树的根节点 root ，树中每个节点都存放有一个 0 到 9 之间的数字。
每条从根节点到叶节点的路径都代表一个数字：

例如，从根节点到叶节点的路径 1 -> 2 -> 3 表示数字 123 。
计算从根节点到叶节点生成的 所有数字之和 。

叶节点 是指没有子节点的节点。
---

#### 思路

``` js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var sumNumbers = function (root) {
  const numbers = []

  const helper = (node, num) => {
    if (!node) {
      return
    }

    const newNum = num * 10 + node.val

    if (!node.left && !node.right) {
      numbers.push(newNum)

      return
    }

    helper(node.left, newNum)
    helper(node.right, newNum)
  }

  helper(root, 0)

  return numbers.reduce((pre, cur) => pre + cur, 0)
};
```
