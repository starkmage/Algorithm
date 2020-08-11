### 11.二进制中1的个数

---

输入一个整数，输出该数32位二进制表示中1的个数。其中负数用补码表示。

---

* 思路

让目标数字和一个数字做与运算；

这个用来比较的数字必须只有一位是1其他位是0，这样就可以知道目标数字的这一位是否为0；

所以用于比较的这个数字初始值为1，比较完后让1左移1位，这样就可以依次比较所有位是否为1。

``` js
function NumberOf1(n)
{
    // write code here
    let count =  0
    let flag = 1
    while (flag) {
        if (flag & n) {
            count++
        }
        flag = flag << 1
    }
    return count
}
```
