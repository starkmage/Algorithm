### 105.从前序与中序遍历序列构造二叉树

---

根据一棵树的前序遍历与中序遍历构造二叉树。

注意:
你可以假设树中没有重复的元素。

例如，给出
```
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
返回如下的二叉树：

    3
   / \
  9  20
    /  \
   15   7
```
---

#### 思路

递归，和“剑指offer-4.重建二叉树”一样

``` js
var buildTree = function(preorder, inorder) {
  if (preorder.length === 0) return null
  let root = new TreeNode(preorder[0])

  let i = inorder.indexOf(preorder[0])

  let preleft = preorder.slice(1, i + 1)
  let preright = preorder.slice(i + 1)

  let inleft = inorder.slice(0, i)
  let inright = inorder.slice(i + 1)

  root.left = buildTree(preleft, inleft)
  root.right = buildTree(preright, inright)
  return root
};
```
