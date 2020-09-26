### 66.机器人的运动范围

---

地上有一个m行和n列的方格。一个机器人从坐标0,0的格子开始移动，每一次只能向左，右，上，下四个方向移动一格，但是不能进入行坐标和列坐标的数位之和大于k的格子。 例如，当k为18时，机器人能够进入方格（35,37），因为3+5+3+7 = 18。但是，它不能进入方格（35,38），因为3+5+3+8 = 19。请问该机器人能够达到多少个格子？

---

* 思路

回溯法

通过深度优先的递归实现，从第一个格开始走，进入递归

1. 判断当前字符是否满足递归终止条件

2. 递归终止条件：(1).行列越界 (2).行列值超出范围 (3).已经走过(需设定一个数组标识当前字符是否走过)

3. 条件不满足，返回0，向上回溯

4. 若上面三个条件都满足，继续向下递归，返回四个方向的递归之和+1（当前节点）

```js
function movingCount(threshold, rows, cols)
{
    // write code here
  //创建一个二维数组，记录是否走过这个格子
  let flag = []
  for (let i = 0; i < rows; i++) {
    flag.push([])
    for (let j = 0; j < cols; j++) {
      flag[i].push(false)
    }
  }
  return moveCount(threshold, rows, cols, flag, 0, 0)
}

function moveCount(threshold, rows, cols, flag, i, j) {
  //递归终止条件：1.越界 2.走过这个格子
  if (i < 0 || i >= rows || j < 0 || j >= cols || flag[i][j]) return 0
  //标记这个格子就走过了
  flag[i][j] = true
  //求这个格子i,j的数位之和
  let sum = 0
  let str = i + '' + j
  for (let k = 0; k < str.length; k++) {
    sum += str[k] * 1
  }
  //递归终止条件：3.数位和超了
  if (sum > threshold) return 0
  //继续递归
  return 1 + moveCount(threshold, rows, cols, flag, i+1, j) + 
    moveCount(threshold, rows, cols, flag, i-1, j) + 
    moveCount(threshold, rows, cols, flag, i, j+1) + 
    moveCount(threshold, rows, cols, flag, i, j-1)
}
```
