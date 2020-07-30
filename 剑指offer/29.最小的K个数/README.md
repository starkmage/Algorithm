### 29.最小的K个数

---

输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4。

---

* 思路1

全排序，然后取出前K个数，直接用JS的`sort()`，因为`sort()`的原理是插入排序和快速排序（数组长度在10以上时），所以可以认为时间复杂度为`O(nlog(n))`

``` JS
function GetLeastNumbers_Solution(input, k)
{
    // write code here
    if (k > input.length || k === 0) return []
    input.sort((a,b) => a - b)
    return input.slice(0, k)
}
```

---

* 思路2
