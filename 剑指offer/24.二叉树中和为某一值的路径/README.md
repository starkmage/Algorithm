### 24.二叉树中和为某一值的路径

---

输入一颗二叉树的根节点和一个整数，按字典序打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。

---

#### 思路1

先进行二叉树路径的遍历，然后选择满足要求的路径。

在遍历二叉树路径时，特别要注意代码中注释的地方。

好理解，但是明显很笨的方法。

``` JS
function FindPath(root, expectNumber)
{
    // write code here
    if(root === null) return [];
    let path = pathTraverse(root);
    let res = path.filter(x => 
        x.reduce((total, value) => total + value) === expectNumber
    );
    
    return res;
}


function pathTraverse(root) {
    if(root === null) return [];    //注意，这里必须是这个，不能是[[]]，这会影响后面的concat以及map
    if(root.left === null && root.right === null) return [[root.val]];
    let left = pathTraverse(root.left);
    let right = pathTraverse(root.right);
    return left.concat(right).map(x => {
        x.unshift(root.val);
        return x;
    })
}
```

---

#### 思路2

直接在递归的时候同时求和

``` js
function FindPath(root, expectNumber)
{
  const path = [], res = []
  var help = function(node, sum) {
    if (!node) return
    path.push(node.val)
    if (node.val === sum && !node.left && !node.right) {
      res.push([...path])
      return
    }
    help(node.left, sum - node.val)
    if (node.left) path.pop()
    help(node.right, sum - node.val)
    if (node.right) path.pop()
  }
  help(root, expectNumber)
  return res
}
```
