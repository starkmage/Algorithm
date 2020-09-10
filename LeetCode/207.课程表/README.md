### 207.课程表

---

你这个学期必须选修 numCourse 门课程，记为 0 到 numCourse-1 。

在选修某些课程之前需要一些先修课程。 例如，想要学习课程 0 ，你需要先完成课程 1 ，我们用一个匹配来表示他们：[0,1]

给定课程总量以及它们的先决条件，请你判断是否可能完成所有课程的学习？

示例 1:
```
输入: 2, [[1,0]] 
输出: true
解释: 总共有 2 门课程。学习课程 1 之前，你需要完成课程 0。所以这是可能的。
```
示例 2:
```
输入: 2, [[1,0],[0,1]]
输出: false
解释: 总共有 2 门课程。学习课程 1 之前，你需要先完成​课程 0；并且学习课程 0 之前，你还应先完成课程 1。这是不可能的。
```
---

#### 思路

这个题之前没有做过类似的，很懵，参考一位大神的[思路](https://leetcode-cn.com/problems/course-schedule/solution/bao-mu-shi-ti-jie-shou-ba-shou-da-tong-tuo-bu-pai-/)

``` js
var canFinish = function(numCourses, prerequisites) {
  const pre = Array(numCourses).fill(0)   // 课程 i 需要提前修的课程门数
  const map = {}  // 记录课程 i 的后续课程编号
  // 统计初始的课程依赖情况
  for (let item of prerequisites) {
    pre[item[0]]++
    if (map[item[1]]) {
      map[item[1]].push(item[0])
    } else {
      map[item[1]] = [item[0]]
    }
  }
  // 把能修的课修掉
  const learned = []
  for (let i in pre) {
    if (pre[i] === 0) learned.push(i)
  }
  // 修完第一轮，开始修后续课程
  let count = 0 // 记录已经修过的课程
  while (learned.length > 0) {
    let temp = learned.shift()
    count++
    let after = map[temp] // 该课程的后续课程
    if (after && after.length) {  // 确实有后续课程
      for (let course of after) {
        pre[course]-- // 该课程的前置课程减一门
        if (pre[course] === 0) {  // 前置课程全部修完，可以修这门课了
          learned.push(course)
        }
      }
    }
  }
  return count === numCourses
};
```
