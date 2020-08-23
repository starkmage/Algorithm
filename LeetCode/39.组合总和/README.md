### 39.组合总和

---

给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的数字可以无限制重复被选取。

说明：

所有数字（包括 target）都是正整数。
解集不能包含重复的组合。 
示例 1：
```
输入：candidates = [2,3,6,7], target = 7,
所求解集为：
[
  [7],
  [2,2,3]
]
```
示例 2：
```
输入：candidates = [2,3,5], target = 8,
所求解集为：
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```
---

#### 思路

回溯算法解决这个问题，剪枝条件也很简单

我觉得这个题最难的地方是如何避免重复数组的问题

在这里用到的方法是设置数组的起始遍历索引start

这样，在往后进行遍历递归的时候，前面的数据不会被遍历到，自然就不会产生重复的结果了

``` js
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum = function(candidates, target) {
  if (candidates.length === 0 || target <= 0) return []
  let res = []
  help(candidates, [], 0, target, res)
  return res
};

function help(arr, temp, start, target, res) {
  //剪枝条件，因为arr都是正数
  if (target < 0) return
  if (target === 0) {
    res.push([...temp])
    return
  }
  for (let i = start; i < arr.length; i++) {
    temp.push(arr[i])
    help(arr, temp, i, target - arr[i], res)
    temp.pop()
  }
}
```
