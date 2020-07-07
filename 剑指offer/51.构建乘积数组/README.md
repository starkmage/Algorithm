### 51.构建乘积数组

---

给定一个数组A[0,1,...,n-1],请构建一个数组B[0,1,...,n-1],其中B中的元素B[i]=A[0]*A[1]*...*A[i-1]*A[i+1]*...*A[n-1]。不能使用除法。（注意：规定B[0] = A[1] * A[2] * ... * A[n-1]，B[n-1] = A[0] * A[1] * ... * A[n-2];）

---

* 思路

可以把B[i]=A[0]A[1]....A[i-1]A[i+1]....A[n-1]。看成A[0]A[1].....A[i-1]和A[i+1].....A[n-2]A[n-1]两部分的乘积。即通过A[i]项将B[i]分为两部分的乘积。

``` JS
function multiply(array)
{
    // write code here
    let res = [];
    if(array.length > 0) {
        res[0] = 1;
        for(let i = 1; i < array.length; i++) {
            res[i] = res[i-1] * array[i-1];
        }
        
        let temp = 1;
        for(let j = array.length - 2; j >= 0; j--) {
            temp *= array[j+1];
            res[j] *= temp;
        }
        
        return res;
    }
}
```
