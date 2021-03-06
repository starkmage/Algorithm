### 31.整数中1出现的次数

---

求出1-13的整数中1出现的次数,并算出100-1300的整数中1出现的次数？为此他特别数了一下1-13中包含1的数字有1、10、11、12、13因此共出现6次,但是对于后面问题他就没辙了。ACMer希望你们帮帮他,并把问题更加普遍化,可以很快的求出任意非负整数区间中1出现的次数（从1 到 n 中1出现的次数）。

---

* 思路

这种问题可以先尝试去归纳一下

1. 个位上

在个位上，每10个数出现一次1,0-9出现1次，10-19出现一次，...，以10为一个阶梯的话，每一个完整的阶梯里面都有一个1,但是对于最后一个不完整的阶梯，比如23，需要分3种情况，当余下的部分>1，则再加一次1，如果小于1，则不能加，等于1，则加1

所以，个位上1的总个数为

`let k = n % 10`

`Math.floor(n / 10) * 1 + if (k > 1) 1      else if (k < 1) 0       else k-1+1`

2. 十位上

在十位上，每100个数出现10次1,0-99出现10次（10-19），100-199出现10次，...，以100为一个阶梯的话，每一个完整的阶梯里面都有10个1,但是对于最后一个不完整的阶梯，比如233，需要分3种情况，当余下的部分>19，则再加10次1，如果小于10，则不能加，在10-19之间，则需要计算确定

所以，十位上1的总个数为

`let k = n % 100`

`Math.floor(n / 100) * 10 + if (k > 19) 10      else if (k < 10) 0       else k-i+1`

3. 更高位数也是同理，归纳出一个公式，i = 1 表示个位，i = 10 表示十位， i = 100 表示百位，则在i位上1的个数为

`let k = n % (i*10)`

`Math.floor(n / (i*10)) * i + if (k > 2*i - 1) i   else if (k < i) 0 else k-i+1`

``` js
function NumberOf1Between1AndN_Solution(n)
{
    // write code here
  if (n < 1) return 0
  let count = 0
  for (let i = 1; i <= n; i *= 10) {
    count += Math.floor(n / (i*10)) * i
    
    let k = n % (i*10)
    if (k < i) {
      count += 0
    } else if (k > 2*i-1) {
      count += i
    } else {
      count += k - i + 1
    }
  }
  return count
}
```
