## 问题
给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。保证base和exponent不同时为0。

## 思路
python做这道题主要是考虑异常
```python
class Solution:
    def Power(self, base, exponent):
        if base == 0:
            return False
        if exponent == 0:
            return 1
        if exponent == 1:
            return base
        flag = False
        if exponent < 0:
            flag = True
        ret = 1
        for i in range(abs(exponent)):
            ret *= base
        if flag:
            return 1/ret
        else:
            return ret
```
指数逐一乘base可以改用二分法代替，例如2^9 = 2^4 * 2^4 * 2，用递归代码如下
```python
class Solution:
    def Power(self, base, exponent):
        if base == 0:
            return False
        if exponent == 0:
            return 1
        if exponent == 1:
            return base
        flag = False
        if exponent < 0:
            flag = True
        ret = self.Power(base, abs(exponent) >> 1)
        ret *= ret
        if exponent & 1 == 1:
            ret *= base
        if flag:
            return 1/ret
        else:
            return ret
```
