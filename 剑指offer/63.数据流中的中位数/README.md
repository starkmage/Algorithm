### 63.数据流中的中位数

---

如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。我们使用Insert()方法读取数据流，使用GetMedian()方法获取当前读取数据的中位数。

---

* 暴力方法

时间复杂度：Insert()为O(1), GetMedian()为O(nlogn)

``` JS
let a = [];

function Insert(num)
{
    // write code here
    a.push(num);
}

function GetMedian(){
	  // write code here
    if(!a) return null;
    
    a.sort((a, b) => a - b);
    
    let center = Math.floor(a.length / 2);
    
    if(a.length % 2 === 0) {
        return (a[center - 1] + a[center]) / 2;
    } else {
        return a[center];
    }
}
```

---

* 插入排序

时间复杂度：Insert()为O(n),即二分查找的O(logn)和挪动数据的O(n), GetMedian()为O(1)。

``` JS
let a = [];

function Insert(num)
{
    // write code here
    
    let i = a.length - 1;
    
    if(i < 0) {
        a.push(num);
    } else {
        while(i >= 0 && a[i] > num) {
            a[i+1] = a[i];
            i--;
        }
        a[i+1] = num;
    }
}

function GetMedian(){
	// write code here
    if(!a) return null;
    
    let center = Math.floor(a.length / 2);
    
    if(a.length % 2 === 0) {
        return (a[center - 1] + a[center]) / 2;
    } else {
        return a[center];
    }
}
```
