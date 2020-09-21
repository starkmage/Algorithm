### 543.二叉树的直径

---

给定一棵二叉树，你需要计算它的直径长度。一棵二叉树的直径长度是任意两个结点路径长度中的最大值。这条路径可能穿过也可能不穿过根结点。

示例 :
```
给定二叉树

          1
         / \
        2   3
       / \     
      4   5    
返回 3, 它的长度是路径 [4,2,1,3] 或者 [5,2,1,3]。
```

注意：两结点之间的路径长度是以它们之间边的数目表示。

---

#### 思路

这道题和“LeetCode-124.二叉树中的最大路径和”思路非常接近，只不过是把求和变成了求长度

注意，题目中说了“两结点之间的路径长度是以它们之间边的数目表示”

在递归的时候，我们在每一项后面长度 + 1，如果下一个节点是 null，那 + 1 不是不应该加吗？是这样处理的，如果为 null，返回 -1，相当于没加

``` js
var diameterOfBinaryTree = function(root) {
  let r = 0
  help(root)
  return r

  function help(node, temp) {
    if (node === null) return -1
    let left = help(node.left) + 1
    let right = help(node.right) + 1
    r = Math.max(r, left + right)
    return Math.max(left, right)
  }
};
```
