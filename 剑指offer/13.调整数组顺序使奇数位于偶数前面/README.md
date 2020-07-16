### 13.调整数组顺序使奇数位于偶数前面

---

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

---

* 思路1

空间换时间，用两个辅助数组，一个放奇数，一个放偶数，这样只需要遍历一次，时间复杂度`O(n)`，空间复杂度`O(n)`。

``` JS
function reOrderArray(array)
{
    // write code here
    let odd = [];
    let even = [];
    for(let num of array) {
        if(num % 2 === 0) {
            even.push(num);
        } else {
            odd.push(num);
        }
    }
    return odd.concat(even);
}
```

* 思路2

插入排序的思想，局部有序的，即局部奇数在前面，偶数在后面，同时保证了稳定性。时间复杂度`O(n^2)`，空间复杂度`O(1)`。

``` JS
function reOrderArray(array)
{
    // write code here
    for(let i = 1; i < array.length; i++) {
        let temp = array[i];
        if(temp % 2 === 1) {
            let j = i - 1;
            while(j >= 0 && array[j] % 2 === 0) {
                array[j+1] = array[j];
                j--;
            }
            array[j+1] = temp;
        }
    }
    return array;
}
```
