### 65.矩阵中的路径

---

请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。

路径可以从矩阵中的任意一个格子开始，每一步可以在矩阵中向左，向右，向上，向下移动一个格子。 如果一条路径经过了矩阵中的某一个格子，则之后不能再次进入这个格子。

例如`a b c e s f c s a d e e`这样的`3 X 4`矩阵中包含一条字符串`"bcced"`的路径，但是矩阵中不包含`"abcb"`路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入该格子。

```
     a b c e 
     s f c s 
     a d e e
```

* 思路

肯定要用到回溯算法，依次验证path中的每个字符（多个步骤），每个字符可能出现在多个方向（多个选项）。

递归结束的条件
  1. 行或者列越界
  2. 字符串不匹配
  3. 矩阵中该位置已经被访问过了
  
成功的条件：
  字符串`path`最后一个字符匹配成功
  
递归不断寻找四个方向是否满足条件，满足条件再忘更深层递归，不满足向上回溯。

如果回溯到最外层，则当前字符匹配失败，将当前字符标记为未走。

``` js
function hasPath(matrix, rows, cols, path) {
    // write code here
    //创建标记是否访问过的标识符矩阵
    let flag = new Array(matrix.length).fill(false)
    for (let i = 0; i < rows; i++) {
        for (let j = 0; j < cols; j++) {
            if (hasPathHelp(matrix, rows, cols, path, i, j, flag, 0)) return true
        }
    }
    return false
}

function hasPathHelp(matrix, rows, cols, path, i, j, flag, k) {
    //矩阵中字符的索引
    const index = i * cols + j
    //递归终止条件
    if (i < 0 || j < 0 || i >= rows || j >= cols || matrix[index] !== path[k] || flag[index]) {
        return false
    }

    //成功匹配所有字符的条件
    if (k === path.length - 1) {
        return true
    }

    flag[index] = true
    
    if (hasPathHelp(matrix, rows, cols, path, i + 1, j, flag, k + 1) ||
        hasPathHelp(matrix, rows, cols, path, i, j + 1, flag, k + 1) ||
        hasPathHelp(matrix, rows, cols, path, i - 1, j, flag, k + 1) ||
        hasPathHelp(matrix, rows, cols, path, i, j - 1, flag, k + 1)) {
        return true
    }
    
    flag[index] = false
    return false
}
```
