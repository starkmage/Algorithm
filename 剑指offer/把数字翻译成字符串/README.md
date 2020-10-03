### 把数字翻译成字符串

---

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

示例 1:
```
输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
```

提示：
```
0 <= num < 231
```

---

#### 动态规划

和青蛙跳台阶一样的思路

``` js
var translateNum = function(num) {
  let str = String(num)
  if (str.length === 1) return 1
  let count = 1
  let dp
  if (str[0] !== 0 && Number(str[0] + str[1]) < 26) dp = [1, 2]
  else dp = [1, 1]
  for (let i = 2; i < str.length; i++) {
    if (str[i - 1] !== '0' && Number(str[i - 1] + str[i]) < 26) dp[i] = dp[i - 1] + dp[i - 2]
    else dp[i] = dp[i - 1]
  }
  return dp[str.length - 1]
};
```
