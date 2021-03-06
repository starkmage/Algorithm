### 96.不同的二叉搜索树

---

给定一个整数 n，求以 1 ... n 为节点组成的二叉搜索树有多少种？

示例:
```
输入: 3
输出: 5
解释:
给定 n = 3, 一共有 5 种不同结构的二叉搜索树:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```
---

#### 动态规划

假设n个节点存在二叉排序树的个数是G(n)，1为根节点，2为根节点，...，n为根节点

当1为根节点时，其左子树节点个数为0，右子树节点个数为n-1

同理当2为根节点时，其左子树节点个数为1，右子树节点为n-2

所以可得G(n) = G(0)*G(n-1)+G(1)*(n-2)+...+G(n-1)*G(0)

``` js
/**
 * @param {number} n
 * @return {number}
 */
var numTrees = function(n) {
  let dp = Array(n + 1).fill(0)
  dp[0] = 1
  dp[1] = 1
  for (let i = 2; i <= n; i++) {
    for (let j = 0; j <= i - 1; j++) {
      dp[i] = dp[i] + dp[j] * dp[i - 1 - j]
    }
  }
  return dp[n]
};
```
