## 问题
输入数字n，按顺序打印出从1到最大的n位十进制数。比如输入3，则打印出1、2、3一直到最大的3位数999。

## 思路
Python中已经对大整数可以进行自动转换了，所以不需要考虑大整数溢出问题。
```python
def printToMaxOfNDigits(n):
    for i in range(10 ** n):
        print(i)
```
