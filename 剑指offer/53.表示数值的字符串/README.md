### 53.表示数值的字符串

---

请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串"+100","5e2","-123","3.1416"和"-1E-16"都表示数值。 但是"12e","1a3.14","1.2.3","+-5"和"12e+4.3"都不是。

---

* 思路1

内置函数，面试不敢写的方法

``` js
//s字符串
function isNumeric(s)
{
    // write code here
    let n = Number(s);
    if (isNaN(n)){
        return false;
    }else {
        return true;
    }
}
```

---

* 思路2

关键是考虑清楚所有情况

1. 只能出现数字、符号位、小数点、指数位

2. 符号位只能出现在开头和指数位后面,还要保证不能出现在结尾

3. 小数点只能出现一次,可以出现在开头结尾，但是出现在结尾前面必须有数字

4. 指数符号只能出现一次、且不能出现在开头结尾

5. 指数符号出现后，小数点不允许再出现，并且指数位后面必须有数字


``` js
function isNumeric(s)
{
    // write code here
  if (s == undefined) return false
  let hasPonit = false
  let hasExp = false
  for (let i = 0; i < s.length; i++) {
    let t = s[i]
    if (t >= 0 && t <= 9) {
      continue
    } else if (t === '+' || t === "-") {
      if ((i === 0 || s[i-1] === "E" || s[i-1] === "e") && i !== s.length - 1) {
        continue
      } else {
        return false
      }
    } else if (t === '.') {
      if (hasPonit || hasExp) {
        return false
      } else if (i === s.length - 1 && (s[i-1] === "+" || s[i-1] === "-")) {
        return false
      } else {
        hasPonit = true
      }
    } else if (t === 'E' || t === 'e') {
      if (i === 0 || i === s.length - 1 || hasExp) {
        return false
      } else {
        hasExp = true
      }
    } else {
      return false
    }
  }
  return true
}
```
