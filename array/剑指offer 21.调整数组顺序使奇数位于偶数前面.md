## 问题
输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

## 思路
书上没有牛客上要求的奇数之间和偶数之间相对位置保持不变，对于书中的情况，代码如下。
```python
class Solution:
    def reOrderArray(self, array):
        if array is None or len(array) < 2:
            return array
        p1, p2 = 0, len(array) - 1
        while p1 < p2:
            while self.isOdd(array[p1]):
                p1 += 1
            while not self.isOdd(array[p2]):
                p2 -= 1
            if p1 < p2:
                array[p1], array[p2] = array[p2], array[p1]
        return array
    
    def isOdd(self, num):
        if num % 2 == 1:
            return True
        return False
```
这里考虑了书中提到的鲁棒性，也就是抽离出判断函数。上述写法不能保证相对顺序，对于牛客的题，解法1是构造两个分别存奇偶数的数组来保存。
```python
class Solution:
    def reOrderArray(self, array):
        odd = []
        even = []
        for i in array:
            if i % 2 == 1:
                odd.append(i)
            else:
                even.append(i)
        return odd + even
```
解法2排序思维。
```python
class Solution:
    def reOrderArray(self, array):
        for i in range(len(array)):
            for j in range(len(array)-1, i, -1):
                if array[j-1] % 2 == 0 and array[j] % 2 == 1:
                    array[j-1], array[j] = array[j], array[j-1]
        return array
```
