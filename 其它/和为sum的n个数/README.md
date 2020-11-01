### 题目描述

从给定的无序、不重复的数组data中，取出n个数，使其相加和为sum。(不需要找到所有的解，找到一个解即可)

### 思路

回溯算法

``` js
var getSum = function(data, n, sum) {
  const temp = []
  var help = function() {
    if (temp.length === n) {
      if (temp.reduce((p, v) => p + v) === sum) return true
      return false
    }
    for (let i = 0; i < data.length; i++) {
      temp.push(data.shift())
      let res = help()
      if (res) return true
      data.push(temp.pop())
    }
  }
  help()
  return temp
}
```
