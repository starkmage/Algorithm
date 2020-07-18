### 1.二维数组中的查找

---

在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

---

* 思路

利用二分查找法，可以把二分值固定在右上角。

当target小于元素a[m][n]时，那么target必定在元素a所在行的左边,即n--；

当target大于元素a[m][m]时，那么target必定在元素a所在列的下边,即m++。

``` JS
function Find(target, array)
{
    // write code here
    let i = array.length;
    if(i === 0) return false;
    let j = array[0].length;
    if(j === 0) return false;
    let m = 0;
    let n = j - 1;
    while(m < i && n >= 0) {
        if(array[m][n] > target) {
            n--;
        } else if(array[m][n] < target) {
            m++;
        } else {
            return true;
        }
    }
    return false;
}
```
