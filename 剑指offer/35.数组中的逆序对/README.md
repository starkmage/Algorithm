### 35.数组中的逆序对

---

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组,求出这个数组中的逆序对的总数P。并将P对1000000007取模的结果输出。 即输出P%1000000007。

---

* 思路

暴力解法行不通，会超时

分治思想，归并排序类似，比归并排序仅多了一行代码，因为要统计次数

``` JS
var reversePairs = function (nums) {
  let count = 0
  mergeSort(nums)
  return count

  // 拆分
  function mergeSort(nums) {
    if (nums.length <= 1) return nums
    let center = Math.floor(nums.length / 2)
    let left = mergeSort(nums.slice(0, center))
    let right = mergeSort(nums.slice(center))
    return merge(left, right)
  }
  // 合并
  function merge(left, right) {
    const res = []
    let i = 0, j = 0
    while (i < left.length && j < right.length) {
      if (left[i] <= right[j]) {
        res.push(left[i])
        i++
      } else {
        res.push(right[j])
        j++
        // 相对于归并排序，添加的唯一一行代码
        count += left.length - i
      }
    }
    while (i < left.length) {
      res.push(left[i])
      i++
    }
    while (j < right.length) {
      res.push(right[j])
      j++
    }
    return res
  }
};
```
