### 32.把数组排成最小的数

---

输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。例如输入数组{3，32，321}，则打印出这三个数字能排成的最小数字为321323。

---

* 思路

这道题的本质就是一种另类的排序方式，如果`字符串 a + b > 字符串 b + a`，则 a 排在 b 后面，我用的是插入排序的方法，其实也可以用JS里的`sort()`函数。

---

``` JS
function PrintMinNumber(numbers)
{
    // write code here
    for(let i = 1; i < numbers.length; i++) {
        let temp = numbers[i];
        let j = i - 1;
        while(j >= 0) {
            let str1 = numbers[j] + "" + temp;
            let str2 = temp + "" + numbers[j];
            if((str1/1) > (str2/1)) {
                numbers[j+1] = numbers[j];
                j--;
            } else {
                break;
            }
        }
        numbers[j+1] = temp;
    }
    return numbers.join('');
}
```

sort 方法

``` js
var minNumber = function(nums) {
  nums.sort((a, b) => {
    let s1 = a + '' + b
    let s2 = b + '' + a
    return s1 - s2
  })
  return nums.join('')
};
```
