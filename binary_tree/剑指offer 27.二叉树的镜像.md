## 问题
操作给定的二叉树，将其变换为源二叉树的镜像。
```
二叉树的镜像定义：源二叉树 
    	    8
    	   /  \
    	  6   10
    	 / \  / \
    	5  7 9 11
    	镜像二叉树
    	    8
    	   /  \
    	  10   6
    	 / \  / \
    	11 9 7  5
```

## 思路
思路很简单，就是从上到下遍历所有树节点，遍历时交换左右子树
```python
class Solution:
    # 返回镜像树的根节点
    def Mirror(self, root):
        if root is not None:
            root.left, root.right = root.right, root.left
            self.Mirror(root.left)
            self.Mirror(root.right)
        return root
```
