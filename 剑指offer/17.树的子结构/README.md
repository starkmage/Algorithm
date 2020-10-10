### 17.树的子结构

---

输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）。

---

* 思路

递归，利用短路

---

``` JS
var isSubStructure = function(A, B) {
  if (A === null || B === null) return false
  return help(A, B) || isSubStructure(A.left, B) || isSubStructure(A.right, B)
};

function help(A, B) {
  if (B === null) return true
  if (A === null || A.val !== B.val) return false
  return help(A.left, B.left) && help(A.right, B.right)
}
```
