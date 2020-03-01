## 问题
请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

## 思路
1. 直接使用python内置函数替换
```python
class Solution:
    # s 源字符串
    def replaceSpace(self, s):
        # write code here
        return s.replace(' ', '%20')
```

2. 使用正则替换
```python
import re

class Solution:
    # s 源字符串
    def replaceSpace(self, s):
        # write code here
        pattern = re.compile(r' ')
        return pattern.sub('%20', s)
```

```python
import re

class Solution:
    # s 源字符串
    def replaceSpace(self, s):
        # write code here
        return re.sub(r'', '%20', s)
```

4. 书中思路，先遍历一遍字符串得到空格数，预留出空格将占用的位置，p2指向替换后的字符串末尾，p1指向原字符串末尾，p1扫到空格前的字符全复制到p2位置，p2前移一格；扫到空格后，p2前移两格
```python
class Solution:
    # s 源字符串
    def replaceSpace(self, s):
        # write code here
        p1 = len(s) - 1
        p2 = len(s) - 1
        rev = range(len(s))[::-1]
        for c in s:
            if c == ' ':
                p2 += 2
        s2 = [''] * (p2 + 1)
        for i in rev:
            if s[i] != ' ':
                s2[p2] = s[p1]
                p2 -= 1
                p1 -= 1
            else:
                s2[p2 - 2:p2] = '%20'
                p2 -= 3
                p1 -= 1
        return ''.join(s2)
```
