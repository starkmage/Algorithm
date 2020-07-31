### 27.字符串的排列

---

输入一个字符串,按字典序打印出该字符串中字符的所有排列。例如输入字符串abc,则按字典序打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。

---

* 思路

1. 使用回溯的思想，个人感觉的难点已经注释；

2. 记录一个字符（temp），用于存储当前需要进入排列的字符，记录一个字符串（current），用于记录当前已经排列好的字符，记录一个队列（queue），用于存储还未被排列的字符；

3. 每次排列将temp添加到current；

4. 如果queue为空，则本次排列完成，将curret加入到结果数组中，结束递归；

5. 如果queue不为空，说明还有未排列的字符；

6. 递归排列queue中剩余的字符；

7. 每次递归完成，将当前递归的字符temp加回队列。

``` js
function Permutation(str)
{
    // write code here
    let result = []
    if (str.length !== 0) {
        let queue = str.split('')
        PermutationHelp(queue, result, '', '')
    }
    //保证是按照字典序排列
    result.sort()
    //如果字符串中有重复的字母，去掉重复的排序
    return [...(new Set(result))]
}

function PermutationHelp(queue, result, temp, current) {
    current += temp
    //说明一次循环到头了，生成了一个完整的字符串
    if (queue.length === 0) {
        result.push(current)
        return
    }
    
    for (let i = 0; i < queue.length; i++) {
        temp = queue.shift()
        PermutationHelp(queue, result, temp, current)
        //这一步是最难理解的，让本轮第一个出去的变成最后一个
        //比如abc循环一轮，变成了bca，这样第二轮循环的时候就是b第一个了
        queue.push(temp)
    }
}
```
