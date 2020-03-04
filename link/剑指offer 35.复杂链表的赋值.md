## 问题
输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针指向任意一个节点），返回结果为复制后复杂链表的head。（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空）

## 思路
```python
class Solution:
    # 返回 RandomListNode
    def Clone(self, pHead):
        if not pHead:
            return None
        
        # Step 1. 复制原始链表任意节点N为新节点N'，并将N'连接到N.next
        orig = pHead
        while orig:
            copy = RandomListNode(orig.label)
            orig.next, copy.next = copy, orig.next
            orig = copy.next
        
        # Step 2. 如果N.random指向一个不为空的节点S，则N'.random指向S'=S.next
        orig = pHead
        while orig:
            copy = orig.next
            if orig.random:
                copy.random = orig.random.next
            orig = copy.next
        
        # Step 3. 分离N，N'
        orig = pHead
        copy_head = pHead.next
        while orig:
            copy = orig.next
            orig.next = copy.next
            orig = orig.next
            if orig:
                copy.next = orig.next
            copy = copy.next
        return copy_head
```
