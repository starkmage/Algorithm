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
  let res = []
  help(root, res, 0)
  return res
};

function help(node, res, i) {
  if (node === null) return
  if (i >= res.length) res.push([])
  res[i].push(node.val)
  help(node.left, res, i + 1)
  help(node.right, res, i + 1)
}
```
