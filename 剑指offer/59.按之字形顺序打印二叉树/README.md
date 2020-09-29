### 59.按之字形顺序打印二叉树

---

请实现一个函数按照之字形打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右至左的顺序打印，第三行按照从左到右的顺序打印，其他行以此类推。

---

* 思路

这个其实和分层打印一样，只不过不同的是需要调整队列中部分数组元素内的元素顺序。

---

``` JS
var levelOrder = function(root) {
  if (root === null) return []
  const res = []
  help(root, res, 1)
  return res
};

function help(node, res, deep) {
  if (node === null) return
  if (deep > res.length) res.push([])
  if (deep % 2 === 1) res[deep - 1].push(node.val)
  else res[deep - 1].unshift(node.val)
  help(node.left, res, deep + 1)
  help(node.right, res, deep + 1)
}
```
