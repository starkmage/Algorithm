### 50.数组中重复的数字

---

在一个长度为n的数组里的所有数字都在0到n-1的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。 例如，如果输入长度为7的数组{2,3,1,0,2,5,3}，那么对应的输出是第一个重复的数字2。

---

* 思路

看到找重复，肯定有一个不错的方法就是map法，但是这个题有一个额外条件：数组里的所有数字都在0到n-1的范围内

所以我们可以构建一个长度为n的数组flag，里面全部初始填充true

在遍历numbers的时候，将flag中numbers[i]位置的变为false，代表这个数字在numbers中遇到过了，下次如果再遇到，证明重复

``` js
function duplicate( numbers ) {
    // write code here
  let len = numbers.length
  let flag = Array(len).fill(true)
  for (let n of numbers) {
    if (flag[n]) flag[n] = false
    else return n
  }
  return -1
}
```
