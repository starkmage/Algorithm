### 6.旋转数组的最小数字

---

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。
输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。
例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。
NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。

---

* 思路

如果直接去Math.min()，等着被挂吧@_@

旋转数组其实是由两个有序数组拼接而成的，可以使用二分法

1. array[mid] > array[end]:

出现这种情况的array类似[3,4,5,6,0,1,2]，此时最小数字一定在mid的右边。 start = mid + 1

2. array[mid] < array[end]:

出现这种情况的array类似[2,2,3,4,5,6,6],此时最小数字一定就是array[mid]或者在mid的左边。因为右边必然都是递增的。 end = mid

3. array[mid] == array[end]:

出现这种情况的array类似 [1,0,1,1,1]或者[1,1,1,0,1]，此时最小数字不好判断在mid左边还是右边,这时只好一个一个试 。 end = end - 1


``` js
function minNumberInRotateArray(rotateArray)
{
    // write code here
    if (rotateArray.length === 0) return 0
    let start = 0
    let end = rotateArray.length - 1
    while (start < end) {
        let mid = Math.floor((start + end)/2)
        if (rotateArray[mid] > rotateArray[end]) {
            start = mid + 1
        } else if (rotateArray[mid] < rotateArray[end]) {
            end = mid
        } else {
            end--
        }
    }
    return rotateArray[end]
}
```
