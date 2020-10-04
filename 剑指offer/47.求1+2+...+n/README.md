### 47.求1+2+...+n

---

求1+2+3+...+n，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

---

#### 思路

数组迭代的方法

---

``` JS
function Sum_Solution(n)
{
    // write code here
    let array = [...Array(n)].map((value, index) => index + 1);
    
    let sum = array.reduce((total, value) => total + value);
    
    return sum;
}
```

#### 递归

``` js
var sumNums = function(n) {
  return n && (n + sumNums(n - 1))
};
```
