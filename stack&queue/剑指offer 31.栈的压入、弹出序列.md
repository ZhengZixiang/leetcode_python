## 问题
输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）

## 思路
遍历popV的写法
```python
class Solution:
    def IsPopOrder(self, pushV, popV):
        if len(pushV) != len(popV) or not pushV:
            return False
        stack = []
        push_index = -1
        for i in popV:
            if stack and stack[-1] == i:
                stack.pop()
                continue
            while True:
                push_index += 1
                if push_index > len(pushV)-1:
                    return False
                if pushV[push_index] == i:
                    break
                stack.append(pushV[push_index])
        return True
```
遍历PushV的写法
```python
class Solution:
    def IsPopOrder(self, pushV, popV):
        # write code here
        if not pushV or len(pushV)!=len(popV):
            return False
        stack=[]
        for i in pushV:
            stack.append(i)
            while len(stack) and stack[-1]==popV[0]:
                stack.pop()
                popV.pop(0)
        if len(stack):
            return False
        return True
```
