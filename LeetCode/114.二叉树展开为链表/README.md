### 114.二叉树展开为链表

---

给定一个二叉树，原地将它展开为一个单链表。

例如，给定二叉树
```
    1
   / \
  2   5
 / \   \
3   4   6
```
将其展开为：
```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```
---

#### 思路

展开的链表的顺序为二叉树先序遍历的顺序

有一个十分巧妙的方法，反向先序遍历递归

``` js
var flatten = function (root) {
  let last = null
  help(root)
  return last
  
  function help(node) {
    if (node === null) return
    help(node.right)
    help(node.left)
    node.right = last
    node.left = null
    last = node
  }
};
```
