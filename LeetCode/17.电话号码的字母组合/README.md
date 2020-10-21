### 17.电话号码的字母组合

---

给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

示例:
```
输入："23"
输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

说明:

尽管上面的答案是按字典序排列的，但是你可以任意选择答案输出的顺序。

---

#### 思路

DFS可以解决这个问题

为了方便，递归过程中str先用数组表示，压入最终结果的时候转变成字符串

``` js
var letterCombinations = function(digits) {
  if (digits.length === 0) return []
  const map = {
    '2': 'abc',
    '3': 'def',
    '4': 'ghi',
    '5': 'jkl',
    '6': 'mno',
    '7': 'pqrs',
    '8': 'tuv',
    '9': 'wxyz'
  }
  const res = []
  let help = function(str, i) {
    if (str.length === digits.length) {
      res.push(str.join(''))
      return
    }
    let temp = map[digits[i]]
    for (let j = 0; j < temp.length; j++) {
      str.push(temp[j])
      help(str, i + 1)
      str.pop()
    }
  }
  help([], 0)
  return res
};
```
