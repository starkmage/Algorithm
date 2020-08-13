### 45.扑克牌顺子

---

LL今天心情特别好,因为他去买了一副扑克牌,发现里面居然有2个大王,2个小王(一副牌原本是54张^_^)...他随机从中抽出了5张牌,想测测自己的手气,看看能不能抽到顺子,如果抽到的话,他决定去买体育彩票,嘿嘿！！“红心A,黑桃3,小王,大王,方片5”,“Oh My God!”不是顺子.....LL不高兴了,他想了想,决定大\小 王可以看成任何数字,并且A看作1,J为11,Q为12,K为13。上面的5张牌就可以变成“1,2,3,4,5”(大小王分别看作2和4),“So Lucky!”。LL决定去买体育彩票啦。 现在,要求你使用这幅牌模拟上面的过程,然后告诉我们LL的运气如何， 如果牌能组成顺子就输出true，否则就输出false。为了方便起见,你可以认为大小王是0。

---

* 思路

1. 遍历一遍，干两件事，（1）统计0的个数，（2）记录最大最小值，（3）查看是否有非0重复值

2. 如果有非0重复的数字，肯定false

3. 0的个数为0,1,2,3的时候，最大值—最小值必须要小于等于4，正好等于4的时候，内部空缺由0填补，小于4的时候0可以填充在两边

4. 0的个数为4，直接成功

``` js
function IsContinuous(numbers)
{
    // write code here
  if (numbers.length === 0 || numbers.length !== 5) return false
  let count = 0
  let max = -Infinity
  let min = Infinity
  for (let i = 0; i < numbers.length; i++) {
    if (numbers[i] === 0) {
      count++
    } else {
      //如果有非0重复，直接失败
      if (numbers.indexOf(numbers[i]) !== i) return false
      if (numbers[i] > max) max = numbers[i]
      if (numbers[i] < min) min = numbers[i]
    }
  }
  //根据0的个数判断
  if (count === 4) return true
  //0个0到4个0情况一致
  if (max - min < 5) return true
  return false
}
```
