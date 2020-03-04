## 问题

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
