### 42.和为S的两个数字

---

输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。

对应每个测试案例，输出两个数，小的先输出。

---

* 思路

1. 双指针法，从两侧向中间紧逼

2. 和相等的两个数字，一定越分散，乘积越小，所以找到第一组后，就不需要继续找了，秒啊

``` js
function FindNumbersWithSum(array, sum)
{
    // write code here
  if (array.length < 2) return []
  let left = 0
  let right = array.length - 1
  while (left < right) {
    let total = array[left] + array[right]
    if (total === sum) {
      //和相等的两个数字，一定越分散，乘积越小，所以不需要继续找了
      return [array[left], array[right]]
    } else if (total < sum) {
      left++
    } else {
      right--
    }
  }
  return []
}
```
