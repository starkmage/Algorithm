### 23.二叉搜索树的后序遍历序列

---

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则输出Yes,否则输出No。假设输入的数组的任意两个数字都互不相同。

---

* 思路

后序序列规律：最后一个值为root；二叉搜索树左子树值都比root小，右子树值都比root大。

1、确定root；

2、遍历序列（除去root结点），找到第一个大于root的位置，则该位置左边为左子树，右边为右子树；

3、遍历左子树和右子树，若发现有不符合规律的值，则直接返回false；

4、分别判断左子树和右子树是否仍是二叉搜索树（即递归步骤1、2、3）。

---

* 递归

``` JS
function VerifySquenceOfBST(sequence)
{
    // write code here
    let len = sequence.length;
    if(len === 0) return false;
    if(len === 1) return true;
    let root = sequence[len-1];
    let index;
    for(let i = 0; i < len; i++) {
        //这里加了等号是应对只有左子树的情况
        if(sequence[i] >= root) {
            index = i;
            break;
        }
    }
    let left = sequence.slice(0, index);
    let right = sequence.slice(index, len-1);
    if(left.length > 0 && right.length > 0) {
        if(Math.max(...left) < root && Math.min(...right) > root) {
            return VerifySquenceOfBST(left) && VerifySquenceOfBST(right);
        } else {
            return false;
        }
    }else if(left.length > 0) {
        if(Math.max(...left) < root) {
            return VerifySquenceOfBST(left);
        } else {
            return false;
        }
    } else if(right.length > 0) {
        if(Math.min(...right) > root) {
            return VerifySquenceOfBST(right);
        } else {
            return false;
        }
    } else {
        return false;
    }
}
```
