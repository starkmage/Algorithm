### 10.矩形覆盖

---

我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？

---

* 思路

画一下前几个，找到规律 f(n) = f(n-1) + f(n-2)，规律类似斐波那契数列。

---

* 递归

``` JS
function rectCover(number)
{
    // write code here
    if(number <= 0) return 0;
    if(number === 1) return 1;
    if(number === 2) return 2;
    
    if(number >= 3) {
        return rectCover(number - 1) + rectCover(number - 2);
    }
}
```

---

* 数组方法（推荐）

``` JS
function rectCover(number)
{
    // write code here
    if(number <= 0) return 0;
    let fib = [1, 2];
    for(let i = 2; i <= number; i++) {
        fib.push(fib[i - 1] + fib[i - 2]);
    }
    return fib[number - 1];
}
```
