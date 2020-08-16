### 52.正则表达式匹配

---
```
请实现一个函数用来匹配包括'.'和'*'的正则表达式。
模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（包含0次）。 
在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但是与"aa.a"和"ab*a"均不匹配。
```
---

* 思路

情况较复杂，可以参考注释

``` JS
function match(s, pattern) {
    // write code here
    if (s.length === 0 && pattern.length === 0) return true
    if (s.length !== 0 && pattern.length === 0) return false
    return matchHelp(s, 0, pattern, 0)
}

function matchHelp(s, i, pattern, j) {
    //1.如果s和pattern都到头了，证明是匹配的
    if (i === s.length && j === pattern.length) return true
    //2.如果s没到头，pattern到头了，一定是不匹配的
    if (i !== s.length && j === pattern.length) return false
    //3.情况比较复杂了
    //3.1如果pattern的下一个字符不是*
    if (pattern[j + 1] !== '*') {
        //3.1.1不匹配，直接false
        if (i < s.length && s[i] !== pattern[j] && pattern[j] !== '.') {
            return false
        } 
        //3.1.2匹配，常规情况递归下一个
        else {
            return matchHelp(s, i + 1, pattern, j + 1)
        }
    } 
    //3.2如果pattern的下一个字符是*
    else {
        //3.2.1如果匹配上了
        if (i < s.length && (s[i] === pattern[j] || pattern[j] === '.')) {
            return matchHelp(s, i + 1, pattern, j) ||   //可能s接下来若干个是重复字符串
                matchHelp(s, i, pattern, j + 2)  //相当于x*被忽略
        } 
        //3.2.2不匹配，*就是0，继续和j+2对比
        else {
            return matchHelp(s, i, pattern, j + 2)
        }
    }
}
```
