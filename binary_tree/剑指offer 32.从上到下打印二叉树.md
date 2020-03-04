## 问题
### 题目一：不分行从上到下打印二叉树
从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

### 题目二：分行从上到下打印二叉树
从上到下按层打印二叉树，同一层的节点按照从左到右的顺序打印，每一层打印一行。

### 题目三：之字形打印二叉树
请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二行按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

## 思路
### 题目一
```python
class Solution:
    # 返回从上到下每个节点值列表，例：[1,2,3]
    def PrintFromTopToBottom(self, root):
        if root is None:
            return []
        queue = [root]
        result = []
        while queue:
            node = queue.pop(0)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
            result.append(node.val)
        return result
```

### 题目二
新增一个统计层节点数的layer_num，该行每打完一个-1，当layer_num为0且队列还有值时，将layer_num赋值为队列长，即下一层节点数
```python
class Solution:
    # 返回二维列表[[1,2],[4,5]]
    def Print(self, pRoot):
        if pRoot is None:
            return []
        queue = [pRoot]
        layer_num = 1
        result = [[]]
        while queue:
            node = queue.pop(0)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
            result[-1].append(node.val)
            layer_num -= 1
            if 0 == layer_num and len(queue) != 0:
                layer_num = len(queue)
                result.append([])
        return result
```

### 题目三
```python
class Solution:
    def Print(self, pRoot):
        if pRoot is None:
            return []
        queue = [pRoot]
        layer_num = 1
        result = [[]]
        left = True  # True表示从左到右打印，False表示从右到左打印，每打完一行改标志位
        while queue:
            node = queue.pop(0)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
            if left: 
                result[-1].append(node.val)
            else:
                result[-1].insert(0, node.val)
            layer_num -= 1
            if 0 == layer_num and len(queue) != 0:
                layer_num = len(queue)
                result.append([])
                left = not left
        return result
```
