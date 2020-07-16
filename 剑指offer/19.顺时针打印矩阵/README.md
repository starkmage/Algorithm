### 19.顺时针打印矩阵

---

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下4 X 4矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.

---

* 思路

顺时针打印就是按圈数循环打印，一圈包含两行或者两列，在打印的时候会出现某一圈中只包含一行，要判断从左向右打印和从右向左打印的时候是否会出现重复打印，同样只包含一列时，要判断从上向下打印和从下向上打印的时候是否会出现重复打印的情况。

---

``` JS
function printMatrix(matrix)
{
    // write code here
    if(matrix.length === 0 || !Array.isArray(matrix[0])) return matrix;
    let res = [];
    //矩阵的长宽
    let l = matrix[0].length;
    let w = matrix.length;
    //圈数
    let n = Math.ceil(Math.min(l, w) / 2);
    for(let m = 0; m < n; m++) {
        //从左上到右上
        for(let i = m; i < l-m; i++) {
            res.push(matrix[m][i]);
        }
        //从右上到右下
        for(let j = m+1; j < w-m-1; j++) {
            res.push(matrix[j][l-1-m]);
        }
        //从右下到左下
        //w-1-m>m是保证与“从左上到右上”不是同一行
        for(let i = l-m-1; i >= m && w-1-m > m; i--) {
            res.push(matrix[w-m-1][i]);
        }
        //从左下到左上
        //l-1-m>m是保证与“从右上到右下”不是同一列
        for(let j = w-m-2; j > m && l-1-m > m; j--) {
            res.push(matrix[j][m])
        }
    。
    return res;
}
```
