### 102.二叉树的层序遍历

---

给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。

示例：
```
二叉树：[3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [9,20],
  [15,7]
]
```
---

#### 思路

利用二叉树的先序遍历，递归实现，不过需要添加一个记录层次位置的 i

和“剑指offer-60.把二叉树打印成多行”一模一样

``` js
var levelOrder = function(root) {
  const res = []
  let help = function(node, deep) {
    if (node === null) return
    if (deep > res.length) res.push([])
    res[deep - 1].push(node.val)
    help(node.left, deep + 1)
    help(node.right, deep + 1)
  }
  help(root, 1)
  return res
};
```

利用队列，BFS

``` js
var levelOrder = function(root) {
  const res = [], queue = []
  if (!root) {
    return []
  }
  queue.push(root)
  while (queue.length) {
    const len = queue.length
    res.push([])
    for (let i = 0; i < len; i++) {
      const node = queue.shift()
      res[res.length - 1].push(node.val)
      if (node.left) {
        queue.push(node.left)
      }
      if (node.right) {
        queue.push(node.right)
      }
    }
  }
  return res
};
```
