### 67.剪绳子

---

给你一根长度为n的绳子，请把绳子剪成整数长的m段（m、n都是整数，n>1并且m>1，m<=n），每段绳子的长度记为k[1],...,k[m]。请问k[1]x...xk[m]可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

---

* 思路

![](https://cdn.jsdelivr.net/gh/starkmage/ImgHosting/starkmage-picgo/Snipaste_2020-08-13_19-27-00.png)


``` js
function cutRope(number)
{
    // write code here
    if(number === 2) return 1
    if(number === 3) return 2
    const mod = number%3
    const count = Math.floor(number/3)
    switch(count) {
        case 0: return Math.pow(3, count)
        case 1: return Math.pow(3, count-1) * 4
        case 2: return Math.pow(3, count) * 2
    }
}
```
