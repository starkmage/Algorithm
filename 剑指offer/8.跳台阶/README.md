### 8.跳台阶

---

一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。

---

* 思路

f(n) = f(n-1) + f(n-2)，规律类似斐波那契数列。

为什么会出现这样的规律呢？
假设现在6个台阶，我们可以从第5跳一步到6，这样的话有多少种方案跳到5就有多少种方案跳到6，另外我们也可以从4跳两步跳到6，跳到4有多少种方案的话，就有多少种方案跳到6，其他的不能从3跳到6什么的啦，所以最后就是f(6) = f(5) + f(4)。

---

* 递归

``` JS
function jumpFloor(number)
{
    // write code here
    if(number <= 0) return 0;
    if(number === 1) return 1;
    if(number === 2) return 2;
    return jumpFloor(number - 1) + jumpFloor(number - 2);
}
```

---

* 数组方法（推荐）

``` JS
function jumpFloor(number)
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
