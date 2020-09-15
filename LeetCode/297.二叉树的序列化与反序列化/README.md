### 297.二叉树的序列化与反序列化

---

序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。

请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。

示例: 

你可以将以下二叉树：
```
    1
   / \
  2   3
     / \
    4   5

序列化为 "[1,2,3,null,null,4,5]"
```
---

#### 思路

和“剑指offer-61.序列化二叉树”基本一致

用的是先序遍历

``` js
/**
 * Encodes a tree to a single string.
 *
 * @param {TreeNode} root
 * @return {string}
 */
var serialize = function(root) {
  // 先序遍历
  if (root === null) return '#'
  let leftStr = serialize(root.left)
  let rightStr = serialize(root.right)
  return root.val + ' ' + leftStr + ' ' + rightStr
};

/**
 * Decodes your encoded data to tree.
 *
 * @param {string} data
 * @return {TreeNode}
 */
var deserialize = function(data) {
  const arr = data.split(' ')
  function help(arr) {
    if (arr.length === 0) return
    let val = arr.shift()
    if (val === '#') return null
    let root = new TreeNode(val)
    root.left = help(arr)
    root.right = help(arr)
    return root
  }
  return help(arr)
};
```
