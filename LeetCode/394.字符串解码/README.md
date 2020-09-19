### 394.字符串解码

---

给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。

示例 1：
```
输入：s = "3[a]2[bc]"
输出："aaabcbc"
```
示例 2：
```
输入：s = "3[a2[c]]"
输出："accaccacc"
```
示例 3：
```
输入：s = "2[abc]3[cd]ef"
输出："abcabccdcdcdef"
```
示例 4：
```
输入：s = "abc3[cd]xyz"
输出："abccdcdcdxyz"
```
---

#### 思路

利用栈结构解决，思路已经在代码中进行了注释

``` js
var decodeString = function(s) {
  const numStack = []
  const charStack = []
  let num = 0
  let res = ''
  for (let char of s) {
    if (!isNaN(char)) {
      num = num * 10 + Number(char) // 读取数字
    } else if (char === '[') {  // 遇到 [
      numStack.push(num)  // 保存次数
      num = 0 // 防止[]内再出现重复，重新开始计数
      charStack.push(res) // 结果压入栈保存
      res = ''  // 重新开始记录 [] 内数字
    } else if (char === ']') {
      let repeatTimes = numStack.pop()  // 重复次数
      res = charStack.pop() + res.repeat(repeatTimes) // 最新结果
    } else {
      res += char
    }
  }
  return res
};
```
