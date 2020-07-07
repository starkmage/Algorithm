### 64.滑动窗口的最大值

---

给定一个数组和滑动窗口的大小，找出所有滑动窗口里数值的最大值。例如，如果输入数组{2,3,4,2,6,2,5,1}及滑动窗口的大小3，那么一共存在6个滑动窗口，他们的最大值分别为{4,4,6,6,6,5}； 针对数组{2,3,4,2,6,2,5,1}的滑动窗口有以下6个： {[2,3,4],2,6,2,5,1}， {2,[3,4,2],6,2,5,1}， {2,3,[4,2,6],2,5,1}， {2,3,4,[2,6,2],5,1}， {2,3,4,2,[6,2,5],1}， {2,3,4,2,6,[2,5,1]}。

---

* 思路

暴力迭代。

``` JS
function maxInWindows(num, size)
{
    // write code here
    if(num.length === 0 || size === 0) return [];
    if(size === 1) return num;
    let res = [];
    for(let i = 0; i <= num.length - size; i++) {
        let temp = num.slice(i, i + size);
        res.push(Math.max(...temp));
    }
    return res;
}
```
