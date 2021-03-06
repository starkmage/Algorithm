### 41.和为S的连续正数序列

---

小明很喜欢数学,有一天他在做数学作业时,要求计算出9~16的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为100(至少包括两个数)。没多久,他就得到另一组连续正数和为100的序列:18,19,20,21,22。现在把问题交给你,你能不能也很快的找出所有和为S的连续正数序列? 

输出所有和为S的连续正数序列。序列内按照从小至大的顺序，序列间按照开始数字从小到大的顺序。

---

* 思路

利用滑动窗口，创造一个容器temp，保存当前累加的值，和为total

1. 如果total大于sum，则需要将total前面的几个数据去掉，具体去掉几个，要根据total何时不大于sum决定

2. 如果total等于sum，则将temp存入result中，至于去掉前面的几个数据，交给下一轮的while循坏执行就可以，非常方便

两个注意点

1. 注意压入temp的时候，深拷贝，否则后续temp的变化影响result内的数据

2. 注意while和if的先后顺序，因为当可能去掉前面几个数据时，剩下数据的和正好等于sum

``` js
function FindContinuousSequence(sum)
{
    // write code here
  if (sum <= 2) return []
  let temp = []
  let total = 0
  let result = []
  for (let i = 1; i <= Math.ceil(sum/2); i++) {
    total += i
    temp.push(i)
    while (total > sum) {
      total -= temp.shift()
    }
    if (total === sum) {
      result.push([...temp])
    }
  }
  return result
}
```

优化一下
``` js
function FindContinuousSequence(sum)
{
  if (sum < 3) return []
  let res = [], temp = []
  let total = 0, start = 0
  for (let i = 1; i <= Math.ceil(sum / 2); i++) {
    total += i
    temp.push(i)
    start = 0
    while (total > sum) {
      total -= temp[start]
      start++
    }
    temp = temp.slice(start)
    if (total === sum) {
      res.push([...temp])
    }
  }
  return res
}
```
