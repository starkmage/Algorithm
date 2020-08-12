### 37.数字在升序数组中出现的次数

---

统计一个数字在升序数组中出现的次数。

---

* JS简洁方法

注意是升序数组，所以相同的数字肯定挨在一起，利用JS中的`indexOf`和`lastIndexOf`，简洁得出答案

``` js
function GetNumberOfK(data, k)
{
    // write code here
  let start = data.indexOf(k)
  if (start === -1) return 0
  let end = data.lastIndexOf(k)
  return end - start + 1
}
```

---

* 二分查找法

利用二分查找，找到下界和上界

下界定义为：如果存在目标值，则指向第一个目标值，否则，如果不存在， 则指向大于目标值的第一个值

上界定义为：不管目标值存在与否，都指向大于目标值的第一个值


``` js
function GetNumberOfK(data, k)
{
    // write code here
  if (data.length === 0) return 0
  //寻找下界
  //下界定义为：如果存在目标值，则指向第一个目标值，否则，如果不存在， 则指向大于目标值的第一个值
  let left = 0
  let right = data.length
  while (left < right) {
    let mid = left + Math.floor((right - left)/2)
    if (data[mid] < k) {
      left = mid + 1
    } else {
      right = mid
    }
  }
  let start = left
  //寻找上界
  //上界定义为：不管目标值存在与否，都指向大于目标值的第一个值
  left = 0
  right = data.length
  while (left < right) {
    let mid = left + Math.floor((right - left)/2)
    if (data[mid] <= k) {
      left = mid + 1
    } else {
      right = mid
    }
  }
  let end = right
  return end - start
}
```
