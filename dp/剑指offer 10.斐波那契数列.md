## 问题
大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0）。

## 思路
1. 递归，会超时。时间复杂度O(n^2)，空间复杂度O(1)。
```python
class Solution:
    def Fibonacci(self, n):
        if n <= 1:
            return n
        return self.Fibonacci(n-1) + self.Fibonacci(n-2)
```
2. n-1和n-2求Fibonacci其实有大量重复计算，于是我们引入数组存储。时间空间复杂度均为O(n)。
```python
class Solution:
    def Fibonacci(self, n):
        if n <= 1:
            return n
        fib = [0] * (n+1)
        fib[0] = 0
        fib[1] = 1
        for i in range(2, n+1):
            fib[i] = fib[i-1] + fib[i-2]
        return fib[n]
```
3. 事实上我们每次只用最近的两个值计算，所以空间可以进一步优化，时间复杂度O(n)，空间复杂度O(1)。
```python
class Solution:
    def Fibonacci(self, n):
        if n <= 1:
            return n
        a = 0
        b = 1
        for i in range(2, n+1):
            fib = a + b
            a = b
            b = fib
        return fib
```
4. 继续优化，上述的fib其实有些冗余，改进一下，时间空间复杂度不变
```python
class Solution:
    def Fibonacci(self, n):
        if n <= 1:
            return n
        a = 0
        b = 1
        for i in range(2, n+1):
            b = a + b
            a = b - a
        return b
```
利用python特性，可以进一步简化为
```python
class Solution:
    def Fibonacci(self, n):
        if n <= 1:
            return n
        a, b = 0, 1
        for i in range(2, n+1):
            a, b = b, a + b
        return b
```
