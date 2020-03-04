## 问题
定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。
注意：保证测试中不会当栈为空的时候，对栈调用pop()或者min()或者top()方法。
## 思路
第一个思路，就是每次往栈中压入一个新元素时，就全栈排序，把最小值置栈顶，但这种思路就不能保证正常的出栈。

第二个思路，是新增一个存储最小值的变量，每次入栈新元素时比较得到最小值，但这种思路再最小值元素pop出去后，不能简单地得到次小值去当最新的最小值。

第三个思路，是第二思路的改进，为了得到最小值，那么新增一个辅助栈，将每次比较的较小值压入栈中，栈顶是最小值，就能在最小元素pop出去后得到新的最小值，代码如下。
```python
class Solution:
    def __init__(self):
        self.stack = []
        self.min_stack = []
    
    def push(self, node):
        if not self.min_stack or self.min_stack[-1] >= node:
            self.min_stack.append(node)
        self.stack.append(node)
        
    def pop(self):
        if self.min_stack[-1] == self.stack[-1]:
            self.min_stack.pop()
        self.stack.pop()
        
    def top(self):
        return self.stack[-1]
    
    def min(self):
        return self.min_stack[-1]
```
