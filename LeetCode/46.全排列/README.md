### 46.全排列

---

给定一个 没有重复 数字的序列，返回其所有可能的全排列。

示例:
```
输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```
---

#### 思路

DFS，本题和剑指offer27题字符串的排列十分类似

1. 比如说 nums 为 [1, 2, 3]进行排列，相当于先把1抽出来，对[2, 3]进行排列，再把2抽出来，对[3]进行排列

2. 当 nums 的长度为 0 时，证明完成一组排列

3. 完成一轮以后，把 3 放回 nums，从 temp 中弹出 3，此时对于只有 3 的 nums 循坏终止（因为 i = 0 小于 nums.length = 1，i + 1便终止了），回到 [2, 3] 的 for 循坏

4. 把 2 放回 nums，nums 变成 [2, 3]，从 temp 中弹出 2，temp 变成 [1]，此时 i + 1变成 1，这次优先压入 3，如此循坏

``` js
var permute = function(nums) {
  const res = []
  let help = function(temp) {
    if (nums.length === 0) {
      res.push([...temp])
      return
    }
    for (let i = 0; i < nums.length; i++) {
      temp.push(nums.shift())
      help(temp)
      nums.push(temp.pop())
    }
  }
  help([])
  return res
};
```
