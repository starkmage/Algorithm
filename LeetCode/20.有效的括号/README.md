### 20.有效的括号

---

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

示例 1:
```
输入: "()"
输出: true
```
示例 2:
```
输入: "()[]{}"
输出: true
```
示例 3:
```
输入: "(]"
输出: false
```
示例 4:
```
输入: "([)]"
输出: false
```
示例 5:
```
输入: "{[]}"
输出: true
```
---

#### 原始思路

是个后进先出的问题，当然要利用栈结构来解决

看起来代码很长，但其实没什么逻辑难度

``` js
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function (s) {
  let stack = []
  for (let i = 0; i < s.length; i++) {
    let char = s[i]
    if (char === '(' || char === '{' || char === '[') {
      stack.push(char)
    } else {
      let top = stack.pop()
      if (char === ')') {
        if (top === '(') {
          continue
        } else {
          return false
        }
      } else if (char === '}') {
        if (top === '{') {
          continue
        } else {
          return false
        }
      } else {
        if (top === '[') {
          continue
        } else {
          return false
        }
      }
    }
  }
  return stack.length === 0 ? true : false
};
```

---

#### 优化思路

其实和原始版本的思路一模一样，只不过是在压入栈的时候，进行了一下转换，很巧妙，这样大幅简化了代码

``` js
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function (s) {
  let stack = []
  for (let i = 0; i < s.length; i++) {
    let char = s[i]
    if (char === '(') {
      stack.push(')')
    } else if (char === '{') {
      stack.push('}')
    } else if (char === '[') {
      stack.push(']')
    } else {
      if (char === stack.pop()) {
        continue
      } else {
        return false
      }
    }
  }
  return stack.length === 0 ? true : false
};
```
