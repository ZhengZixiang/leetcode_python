## 问题
输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。

## 思路
首先明确是左右子树深度递归的思路，当左右子树分别排好序后，左子树应该右移到最右节点拼接到根节点，右子树应该左移到最左节点拼接到根节点，再向上返回，返回时根节点又要左移到最左节点（程序最终要求头节点是最小节点）
```python
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
class Solution:
    def Convert(self, pRootOfTree):
        if not pRootOfTree:
            return None
        if not pRootOfTree.left and not pRootOfTree.right:
            return pRootOfTree
        
        pre = post = None
        if pRootOfTree.left:
            pre = self.Convert(pRootOfTree.left)
            while pre.right:
                pre = pre.right
        if pRootOfTree.right:
            post = self.Convert(pRootOfTree.right)
            while post.left:
                post = post.left
                
        if pre:
            pRootOfTree.left, pre.right = pre, pRootOfTree
        if post:
            pRootOfTree.right, post.left = post, pRootOfTree
            
        while pRootOfTree.left:
            pRootOfTree = pRootOfTree.left
        return pRootOfTree
```
