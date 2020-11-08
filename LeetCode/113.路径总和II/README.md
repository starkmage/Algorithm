### 113.路径总和II

---

给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

说明: 叶子节点是指没有子节点的节点。

示例:
给定如下二叉树，以及目标和 sum = 22，

```

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
返回:

[
   [5,4,11,2],
   [5,8,4,5]
]
```

---

#### 思路

递归，联系112,437看，和“剑指offer--24题一样”

``` js
var pathSum = function(root, sum) {
  if (root === null) return []
  const res = []
  var help = function(node, temp, sum) {
    if (node === null) return
    temp.push(node.val)
    if (node.val === sum && node.left === null && node.right === null) {
      res.push([...temp])
    }
    help(node.left, temp, sum - node.val)
    help(node.right, temp, sum - node.val)
    temp.pop()
  }
  help(root, [], sum)
  return res
};
```
