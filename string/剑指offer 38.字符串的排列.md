## 问题
输入一个字符串,按字典序打印出该字符串中字符的所有排列。例如输入字符串abc,则打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。

## 思路
思路就是递归，每次固定一个字母，然后剩下的字母求全排列。
```python
class Solution:
    def Permutation(self, ss):
        if not ss:
            return []
        if len(ss) == 1:
            return [ss]
            
        sub_per_set = set()
        for i in range(0, len(ss)):
            sub_ss = ss[0:i] + ss[i+1:len(ss)]
            sub_per = self.Permutation(sub_ss)
            for j in range(0, len(sub_per)):
                sub_per[j] = ss[i] + sub_per[j]
            sub_per_set.update(set(sub_per))
        return sorted(list(sub_per_set))
```
还有就是用python自带工具函数
```python
import itertools
class Solution:
    def Permutation(self, ss):
        if not ss:
            return []
        return sorted(list(set(map(''.join, itertools.permutations(ss)))))
```
