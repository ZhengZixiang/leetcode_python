## 问题
输入一个链表的头节点，从尾到头反过来打印出每个节点的值。

## 思路
1. 栈操作，这里简单地使用了列表反转，也可以用res.insert(0, listNode.val)
```python
class Solution:
    # 返回从尾部到头部的列表值序列，例如[1,2,3]
    def printListFromTailToHead(self, listNode):
        res = []
        while listNode is not None:
            res.append(listNode.val)
            listNode = listNode.next
        return res[::-1]
```

2. 递归，递归本质上就是一种栈操作
```python
class Solution:
    # 返回从尾部到头部的列表值序列，例如[1,2,3]
    def printListFromTailToHead(self, listNode):
        res = []
        def printNode(listNode):
            if listNode is not None:
                printNode(listNode.next)
                res.append(listNode.val)
        printNode(listNode)
        return res
```
