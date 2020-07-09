### 54.字符流中第一个不重复的字符

---

请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符"go"时，第一个只出现一次的字符是"g"。当从该字符流中读出前六个字符“google"时，第一个只出现一次的字符是"l"。如果当前字符流没有存在出现一次的字符，返回#字符。


---

* 思路

运用哈希表或者对象。

---

``` JS
let map = {};
//Init module if you need\
function Init()
{
    // write code here
    map = {};
}


//Insert one char from stringstream
function Insert(ch)
{
    // write code here
    if(map[ch]) {
        map[ch]++;
    } else {
        map[ch] = 1;
    }
}


//return the first appearence once char in current stringstream
function FirstAppearingOnce()
{
    // write code here
    let s = "#";
    for(let key in map) {
        if(map[key] === 1) {
            s = key;
            break;
        }
    }
    return s;
}
```
