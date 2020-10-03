### 29.最小的K个数

---

输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4。

---

* sort()

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

* 快速排序

``` js
var getLeastNumbers = function(arr, k) {
  if (arr.length < k) return arr
  quickSort(arr, 0, arr.length - 1)
  return arr.slice(0, k)
};

function quickSort(arr, left, right) {
  if (left >= right) return
  let temp = arr[left]
  let i = left, j = right
  while (left < right) {
    while (left < right && temp <= arr[right]) right--
    arr[left] = arr[right]
    while (left < right && temp >= arr[left]) left++
    arr[right] = arr[left]
  }
  arr[left] = temp
  quickSort(arr, i, left - 1)
  quickSort(arr, left + 1, j)
}
```

---

* 大顶堆

把input的前K个数建立一个大顶堆，从第K个数开始，和大顶堆的最大值进行比较，若比最大值小，交换两个数的位置，重新构建大顶堆，最终大顶堆就是最小的K个数，时间复杂度`O(nlogK)`

``` JS
function GetLeastNumbers_Solution(input, k) {
    // write code here
    if (k > input.length || k === 0) return []
    createMaxHeap(input, k)
    for (let i = k; i < input.length; i++) {
        if (input[i] < input[0]) {
            [input[0], input[i]] = [input[i], input[0]]
            adjustMaxHeap(input, 0, k)
        }
    }
    return input.slice(0, k)
}

function createMaxHeap(arr, length) {
    //最后一个非叶子节点
    let mid = Math.floor(length / 2) - 1
    for (let i = mid; i >= 0; i--) {
        adjustMaxHeap(arr, i, length)
    }
}

function adjustMaxHeap(arr, index, length) {
    for (let i = 2 * index + 1; i < length; i = 2 * i + 1) {
        if (i + 1 < length && arr[i + 1] > arr[i]) {
            i++
        }
        if (arr[i] > arr[index]) {
            [arr[index], arr[i]] = [arr[i], arr[index]]
            index = i
        } else {
            break
        }
    }
}
```
