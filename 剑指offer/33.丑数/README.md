### 33.丑数

---

把只包含质因子2、3和5的数称作丑数（Ugly Number）。例如6、8都是丑数，但14不是，因为它包含质因子7。 习惯上我们把1当做是第一个丑数。求按从小到大的顺序的第N个丑数。

---

* 思路

如果p是丑数，那么p=2^x * 3^y * 5^z，后面的丑数肯定是前面某一一个丑数乘以2，3，5中的一个得来的，并且是得到最小的那个数，那么就可以用动态规划来解决这个问题。

要注意一个问题，比如丑数6，可以由 t2 = 2, uglyNum[t2] * 2得到，也可以由 t3 = 1, uglyNum[t3] * 3得到，所以后面 t2 和 t3都需要加1。

---

``` JS
function GetUglyNumber_Solution(index)
{
    // write code here
    if(index <= 0) return 0;
    let [t2, t3, t5] = [0, 0, 0];
    let uglyNum = [1];
    for(let i = 1; i < index; i++) {
        uglyNum[i] = Math.min(uglyNum[t2] * 2, uglyNum[t3] * 3, uglyNum[t5] * 5);
        
        if(uglyNum[i] === uglyNum[t2] * 2) t2++;
        if(uglyNum[i] === uglyNum[t3] * 3) t3++;
        if(uglyNum[i] === uglyNum[t5] * 5) t5++;
    }
    return uglyNum[index-1];
}
```
