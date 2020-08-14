### 28.数组中出现次数超过一半的数字

---

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。

如果不存在则输出0。

---

* 哈希法

空间换时间，开辟一个哈希表记录数字出现的次数，时间复杂度`O(n)`，空间复杂度`O(n)`

``` js
function MoreThanHalfNum_Solution(numbers)
{
    // write code here
  if (numbers.length === 0) return 0
  let map = {}
  numbers.forEach(value => {
    if (map[value]) {
      map[value]++
    } else {
      map[value] = 1
    }
  })
  for (let item in map) {
    if (map[item] > numbers.length/2) {
      return item
    }
  }
  return 0
}
```

---

* 排序法

先将数组排序，可能的结果一定在数组中间，不过，还需要验证一次

时间复杂度`O(nlogn)`，空间复杂度`O(1)`

``` js
function MoreThanHalfNum_Solution(numbers)
{
    // write code here
  if (numbers.length === 0) return 0
  numbers.sort((a, b) => a - b)
  let mid = Math.floor(numbers.length / 2)
  let maybe = numbers[mid]
  let count = 0
  numbers.forEach(value => {
    if (value === maybe) {
      count++
    }
  })
  return count > numbers.length / 2 ? maybe : 0
}
```

---

* 候选法

最优方法，思路较复杂，时间复杂度`O(nlogn)`，空间复杂度`O(1)`

记录两个变量————数组中的某个值 & 次数

1.当前遍历值和上一次遍历值相等？次数+1 ： 次数-1

2.次数变为0后保存新的值

3.遍历结束后保存的值,验证其是否符合条件

最坏情况下，每次消去一个众数和一个非众数，那么如果存在众数，最后留下的数肯定是众数

``` js
function MoreThanHalfNum_Solution(numbers)
{
    // write code here
  if (numbers.length === 0) return 0
  let flag = numbers[0]
  let count = 1
  for (let i = 1; i < numbers.length; i++) {
    if (numbers[i] !== flag) {
      count--
      if (count === 0) {
        flag = numbers[i]
        count = 1
      }
    } else {
      count++
    }
  }

  count = 0
  numbers.forEach(value => {
    if (value === flag) count++
  })
  return count > numbers.length / 2 ? flag : 0
}
```
