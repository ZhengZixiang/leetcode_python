## 问题
输入一个链表，输出该链表中倒数第k个结点。

## 思路
1. 先遍历一遍链表得到链表长度n，则再从头遍历n-k+1个节点就是目标节点，但是这种做法是O(2N)。
2. 快慢指针的思路，快指针先走k-1步，然后快慢指针再一起一步步后移，当快指针next为空时，刚好慢指针指向倒数第k个节点。需要注意几个特殊情况处理，k<=0和头指针为空，直接返回None。当链表长度不足k时，也返回None，即快指针先走k-1步中一旦next为None，直接返回None，时间复杂度O(N)。
```python
class Solution:
    def FindKthToTail(self, head, k):
        if head is None or k <= 0:
            return None
        fast = slow = head
        for i in range(k - 1):
            if fast.next is not None:
                fast = fast.next
            else:
                return None
        while fast.next is not None:
            fast = fast.next
            slow = slow.next
        return slow
```
