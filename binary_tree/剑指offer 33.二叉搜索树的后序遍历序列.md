## 问题
输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则输出True，否则输出False。假设输入的数组的任意两个数字都互不相同。

## 思路
后序遍历数组的最后一个值是根节点，以根节点为划分找左右子数组是否分别均小于\大于根节点，若是，将子数组进行递归判断。
```python
class Solution:
    def VerifySequenceOfBST(self, sequence):
        if not sequence:
            return False
        root = sequence[-1]
        idx = 0
        while sequence[idx] < root:
            idx += 1
        for i in range(idx, len(sequence) - 1):
            if sequence[i] < root:
                return False
        
        left = right = True
        left_seq = sequence[0:idx]
        right_seq = sequence[idx:-1]
        if len(left_seq) > 0:
            left = self.VerifySequenceOfBST(left_seq)
        if len(right_seq) > 0:
            right = self.VerifySequenceOfBST(right_seq)
        return left and right
```
