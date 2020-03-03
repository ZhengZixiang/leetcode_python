## 问题
请实现一个函数，用来判断一颗二叉树是不是对称的。注意，如果一个二叉树同此二叉树的镜像是同样的，定义其为对称的。

## 思路
递归判断前序遍历和对称前序遍历是否一样
```python
class Solution:
    def isSymmetrical(self, pRoot):
        return self.judge_subtree(pRoot, pRoot)
    
    def judge_subtree(self, pRoot1, pRoot2):
        if pRoot1 is None and pRoot2 is None:
            return True
        if pRoot1 is None or pRoot2 is None:
            return False
        if pRoot1.val != pRoot2.val:
            return False
        return self.judge_subtree(pRoot1.left, pRoot2.right) and \
               self.judge_subtree(pRoot1.right, pRoot2.left)
```
