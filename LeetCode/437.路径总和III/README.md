### 437.路径总和III

---

给定一个二叉树，它的每个结点都存放着一个整数值。

找出路径和等于给定数值的路径总数。

路径不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

二叉树不超过1000个节点，且节点数值范围是 [-1000000,1000000] 的整数。

示例：
```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

返回 3。和等于 8 的路径有:

1.  5 -> 3
2.  5 -> 2 -> 1
3.  -3 -> 11
```
---

#### 思路

双重递归思路，

首先先序递归遍历每个节点，

再以每个节点作为起始点递归寻找满足条件的路径

这个题注意联系“剑指offer-24.二叉树中和为某一值的路径”

``` js
var pathSum = function(root, sum) {
  if (root === null) return 0
  let count = getSum(root, sum)
  let leftCount = pathSum(root.left, sum)
  let rightCount = pathSum(root.right, sum)
  return count + leftCount + rightCount
};

function getSum(node, sum) {
  if (node === null) return 0
  let now = node.val === sum ? 1 : 0
  let leftSum = getSum(node.left, sum - node.val)
  let rightSum = getSum(node.right, sum - node.val)
  return now + leftSum + rightSum
}
```
