### 337.打家劫舍

---

在上次打劫完一条街道之后和一圈房屋后，小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为“根”。 除了“根”之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果两个直接相连的房子在同一天晚上被打劫，房屋将自动报警。

计算在不触动警报的情况下，小偷一晚能够盗取的最高金额。

示例 1:
```
输入: [3,2,3,null,3,null,1]

     3
    / \
   2   3
    \   \ 
     3   1

输出: 7 
解释: 小偷一晚能够盗取的最高金额 = 3 + 3 + 1 = 7.
```
示例 2:
```
输入: [3,4,5,1,3,null,1]

     3
    / \
   4   5
  / \   \ 
 1   3   1

输出: 9
解释: 小偷一晚能够盗取的最高金额 = 4 + 5 = 9.
```
---

#### 递归

* 对于一个以 node 为根节点的二叉树而言，如果尝试偷取 node 节点，那么势必不能偷取其左右子节点，然后继续尝试偷取其左右子节点的左右子节点。

* 如果不偷取该节点，那么只能尝试偷取其左、右子节点。当然，没打劫父节点也不一定就非得打劫它的子节点。

* 比较两种方式的结果，谁大取谁。

``` js
var rob = function(root) {
  if (root === null) return 0
  // 抢劫父节点
  let selected = root.val
  if (root.left) {
    selected += rob(root.left.left) + rob(root.left.right)
  }
  if (root.right) {
    selected += rob(root.right.left) + rob(root.right.right)
  }
  // 不抢劫父节点
  let notSelected = rob(root.left) + rob(root.right)
  return Math.max(selected, notSelected)
};
```

---

#### 动态规划（优化版）

大致思路是一样的

我们知道，打劫一个树的最大收益，是 selected 和 notSelected 中的较大者。

即每个子树都有两个状态下的最优解：打劫 root 和没打劫 root 下的最优解。

我们用一个数组记录这个状态

``` js
var rob = function(root) {
  function help(node) {
    if (node === null) return [0, 0]
    const left = help(node.left)
    const right = help(node.right)
    const selected = node.val + left[1] + right[1]
    // 没打劫父节点
    const notSelected = Math.max(left[0], left[1]) + Math.max(right[0], right[1])
    return [selected, notSelected]
  }
  const res = help(root)
  return Math.max(res[0], res[1])
};
```
