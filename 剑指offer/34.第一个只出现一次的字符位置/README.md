### 34.第一个只出现一次的字符位置

---

在一个字符串(0<=字符串长度<=10000，全部由字母组成)中找到第一个只出现一次的字符,并返回它的位置, 如果没有则返回 -1（需要区分大小写）.（从0开始计数）

---

* Hash解法

``` JS
function FirstNotRepeatingChar(str)
{
    // write code here
    if(str.length === 0) return -1;
    let map = {};
    for(let i = 0; i < str.length; i++) {
        if(map.hasOwnProperty(str[i])) {
            map[str[i]]++;
        }else {
            map[str[i]] = 1;
        }
    }
    for(let key in map) {
        if(map[key] === 1) {
            return str.indexOf(key);
        }
    }
    return -1;
}
```

---

* 一种更简洁的方法

``` JS
function FirstNotRepeatingChar(str)
{
    // write code here
    if(str.length === 0) return -1;
    for(let i = 0; i < str.length; i++) {
        if(str.indexOf(str[i]) === str.lastIndexOf(str[i])) {
           return i;
        }
    }
    return -1;
}
