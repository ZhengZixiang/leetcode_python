## 问题
输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。

## 思路
注意到这道题在python中与在Java和C有很大的不同，对于Java或者C这样数值类型有固定长度类型的语言，一个负数n不断和(n-1)做与运算，值会不断变小，但最终会下溢变成0，所以循环最终会退出。而python中的数字类型是没有长度限制的。所以python一个负数n和(n-1)相与的话，会不断增大，导致了死循环。

1. 当输入的数是正整数，一个很直觉的想法就是一直右移，每次右移&1。
```python
class Solution:
    def NumberOf1(self, n):
        count = 0
        while n > 0:
            if n & 1:
                count += 1
            n = n >> 1
        return count
```
其实上述解法在python中由于上述问题而无法跑通，需要人为限制右移32次。
```python
class Solution:
    def NumberOf1(self, n):
        return sum([(n >> i) & 1 for i in range(32)])
```
2. 但上述解法无法处理负数情况，例如0x8000000，右移后并不是变成正数0x40000000了，而是保持最高位为负数标志，变为0xC000000，一直右移最后会变成0xFFFFFFFF陷入死循环。一种常规解法是，从1到2的位数次方，每个数都与n与一次
```python
class Solution:
    def NumberOf1(self, n):
        count = 0
        for i in range(0, 32):
            if (1 << i) & n > 0:
                count += 1
        return count
```
3. 最佳解法
n & (n-1)=n去掉最后一个1，这个性质背起来，则有如下解法，这里比书上多了一步操作，正是思路一开始提到的python特性，把n和0xffffffff相与，相当于把一个负数变成与其二进制表示相同的正数，这样就不会出现上面的问题。
```python
class Solution:
    def NumberOf1(self, n):
        count = 0
        if n < 0:
            n = n & 0xffffffff
        while n:
            count += 1
            n = (n - 1) & n
        return count
```
