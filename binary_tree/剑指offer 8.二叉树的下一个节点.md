## 问题
给定一个二叉树和其中的一个结点，请找出中序遍历顺序的下一个结点并且返回。注意，树中的结点不仅包含左右子结点，同时包含指向父结点的指针。

## 思路
如剑指，建议看书
```python
class Solution:
    def GetNext(self, pNode):
        # 如果一个节点有右子树，那么该节点中序遍历的下一个节点就是右子树的最左子节点
        if pNode.right:
            next = pNode.right
            while next.left:
                next = next.left
            return next
        # 如果一个节点无右子树，且该节点是父节点的左子节点，那么它的下一个节点就是父节点
        if pNode.next and pNode.next.left == pNode:
            return pNode.next
        # 如果一个节点无右子树，且该节点是父节点的右子节点，那就上溯到第一个不在"父节点的右节点"的祖宗节点
        if pNode.next and pNode.next.right == pNode:
            next = pNode.next
            while next.next and next.next.right == next:
                next = next.next
            return next.next
        return None
```
实际上2 3步的判断逻辑可以合并，则如下
```python
class Solution:
    def GetNext(self, pNode):
        if pNode.right:
            next = pNode.right
            while next.left:
                next = next.left
            return next

        while pNode.next:
            if pNode.next.left == pNode:
                return pNode.next
            pNode = pNode.next
        return None
```
