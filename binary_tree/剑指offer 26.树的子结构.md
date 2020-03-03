## 问题
输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）。

## 思路
若A，B根节点值相同，则开始判断B是不是A子树，否则，判断A的左右子树里是否有B
```python
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
class Solution:
    def HasSubtree(self, pRoot1, pRoot2):
        if pRoot1 is None or pRoot2 is None:
            return False
        return self.HasSubtree(pRoot1.left, pRoot2) or \
               self.HasSubtree(pRoot1.right, pRoot2) or \
               self.dose_tree1_have_tree2(pRoot1, pRoot2)
        
    
    def dose_tree1_have_tree2(self, pRoot1, pRoot2):
        if pRoot2 is None:
            return True
        if pRoot1 is None or pRoot1.val != pRoot2.val:
            return False
        return self.dose_tree1_have_tree2(pRoot1.left, pRoot2.left) and \
               self.dose_tree1_have_tree2(pRoot1.right, pRoot2.right)
```
