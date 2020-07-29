### 35.数组中的逆序对

---

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组,求出这个数组中的逆序对的总数P。并将P对1000000007取模的结果输出。 即输出P%1000000007。

---

* 思路

暴力解法行不通，会超时

分治思想，归并排序类似，比归并排序要复杂，因为要统计次数

``` JS
let count = 0

function InversePairs(data)
{
    // write code here
    if(data.length < 2) return 0
    mergeSort(data, 0, data.length-1)
    return count%1000000007
}

function mergeSort(arr,start,end) {
    if(start === end) return
    let mid = Math.floor((start+end)/2)
    mergeSort(arr,start,mid)
    mergeSort(arr,mid+1,end)
    merge(arr,start,mid,end)
}

function merge(arr,start,mid,end) {
    let temp = []
    let t = 0
    let i = start
    let j = mid+1
    
    while(i <= mid && j <= end) {
        if(arr[i] <= arr[j]) {
            temp[t++] = arr[i++]
        } else {
            temp[t++] = arr[j++]
            count += mid-i+1
        }
    }
    
    while(i <= mid) {
        temp[t++] = arr[i++]
    }
    while(j <= end) {
        temp[t++] = arr[j++]
    }
    
    //把临时数组的顺序还原给arr
    let k = start
    let m = 0
    while(k <= end) {
        arr[k++] = temp[m++]
    }
}
```
