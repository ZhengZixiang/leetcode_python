## 问题
请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串"+100","5e2","-123","3.1416"和"-1E-16"都表示数值。 但是"12e","1a3.14","1.2.3","+-5"和"12e+4.3"都不是。

## 思路
1. Python自带转化数字
```python
class Solution:
    # s字符串
    def isNumeric(self, s):
        try:
            f = float(s)
            return True
        except:
            return False
```
2. 正则表达式
```python
import re

class Solution:
    # s字符串
    def isNumeric(self, s):
        return re.match(r'^[\+\-]?\d*(\.\d+)?([eE][\+\-]?[0-9]+)?$', s)
```
