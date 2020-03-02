## 问题
### 题目1
给定单向链表的头指针和一个节点指针，定义一个函数在O(1)时间内删除该节点。
### 题目2
在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。 例如，链表1->2->3->3->4->4->5 处理后为 1->2->5。

## 思路
题意不难，但是链表思路要清晰，代码要准确
### 题目1
牛客没有题目1的OJ，所以这里代码只是参考书上写的伪代码，不保证正确。
```python
class Solution:
    def deleteNode(pListHead, pToBeDeleted):
        if pListHead is None or pToBeDeleted is None:
            return
        # 链表只有一个节点，删除头结点即可
        if pListHead == pToBeDeleted:
            del pListHead
        # 要删除的节点不是尾节点
        if pToBeDeleted.next:
            pNext = pToBeDeleted.next
            pToBeDeleted.val = pNext.val
            pToBeDeleted.next = pNext.next
            del pNext
        # 若是尾节点，则只能遍历
        else:
            pNode = pListHead
            while pNode:
                if pNode.next == pToBeDeleted:
                    pNode.next = None
                pNode = pNode.next         
```

### 题目2
注意这里不是保留一个重复的节点，而是所有重复的节点都删除。要特别注意处理头为空、头节点next为空，和头节点即重复的特殊情况。要创造一个新的头节点指向pHead，方便计算。
```python
class Solution:
    def deleteDuplication(self, pHead):
        if pHead is None or pHead.next is None:
            return pHead
        Head = ListNode(-1)
        Head.next = pHead
        pPre, pCur = Head, pHead
        while pCur:
            if pCur.next and pCur.next.val == pCur.val:
                while pCur.next and pCur.next.val == pCur.val:
                    pCur = pCur.next
                pPre.next, pCur = pCur.next, pCur.next
            else:
                pPre, pCur = pCur, pCur.next
        return Head.next
```
