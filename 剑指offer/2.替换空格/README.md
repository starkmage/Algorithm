### 2.替换空格

---

请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

---

* 思路

直接用JS中的`正则表达式+repalce`，一行代码解决。

``` JS
function replaceSpace(str)
{
    // write code here
    return str.replace(/\s/g, "%20");
}
