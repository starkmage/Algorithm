### 49.把字符串转换成整数

---

将一个字符串转换成一个整数，要求不能使用字符串转换整数的库函数。 数值为0或者字符串不是一个合法的数值则返回0。

输入描述:

输入一个字符串,包括数字字母符号,可以为空。

输出描述:

如果是合法的数值表达则返回该数字，否则返回0。

---

* 示例

输入：

+2147483647

1a33

输出：

2147483647

0

---

* 思路

要求不能使用字符转换成数字的库函数，所以可以巧妙运用`"x"/1`是一个数字的方法。

``` JS
function StrToInt(str)
{
    // write code here
    let flag = 1;
    let ans = 0;
    for(let i = 0; i < str.length; i++) {
        let s = str[i];
        if(i === 0 && s === "-") {
            flag = -1;
            continue;
        } else if(i === 0 && s === "+") {
            continue;
        }
        
        if(s >= "0" && s <= "9") {
            ans = ans*10 + s/1;
        } else {
            return 0;
        }
    }
    return flag * ans;
}
```
