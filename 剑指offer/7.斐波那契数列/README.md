### 7.斐波那契数列

---

大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0，第1项是1）。n<=39

---

* 数列方法

``` JS

function Fibonacci(n)
{
    // write code here
    if(n <= 0) return 0;
    let fib = [1, 1];
    for(let i = 2; i <= n; i++) {
        fib.push(fib[i - 1] + fib[i - 2]);
    }
    return fib[n - 1];
}
```
