### 62.二叉搜索树的第k个节点

---

给定一棵二叉搜索树，请找出其中的第k小的结点。例如， （5，3，7，2，4，6，8）    中，按结点数值大小顺序第三小结点的值为4。

---

* 思路

二叉搜索树的中序遍历得到的结果就是从小到大排列的，可以利用这一点。

``` JS
function KthNode(pRoot, k)
{
  const res = []
  function tarverse(root) {
    if (root === null) return
    tarverse(root.left)
    res.push(root)
    tarverse(root.right)
  }
  tarverse(pRoot)
  return res[k - 1]
}
```
