### 12.数值的整数次方

---

给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

保证base和exponent不同时为0。

---

#### 暴力

面试的时候敢不敢这么写是个问题

``` js
function Power(base, exponent)
{
    // write code here
  return base ** exponent
}
```

#### 常规累乘

时间复杂度为`O(n)`，虽然不是最优解法（最优解法是递归，O(logn)），但是最好理解

``` js
function Power(base, exponent)
{
    // write code here
  //0的0次方等于1
  if (exponent === 0) return 1
  if (base === 0) return 0
  let res = 1
  if (exponent > 0) {
    for (let i = 0; i < exponent; i++) {
      res *= base
    }
    return res
  }
  if (exponent < 0) {
    for (let i = 0; i < Math.abs(exponent); i++) {
      res *= base
    }
    return 1/res
  }
}
```

#### 递归

``` js
var myPow = function(x, n) {
  if (n === 0) return 1
  if (x === 0) return 0
  if (n < 0) {
    x = 1 / x
    n = -n
  }
  return n % 2 === 0 ? myPow(x * x, n / 2) : myPow(x * x, (n - 1) / 2) * x
};
```
