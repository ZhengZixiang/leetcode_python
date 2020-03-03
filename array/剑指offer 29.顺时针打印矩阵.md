## 问题
输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，

例如，如果输入如下4 X 4矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16

则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.

## 思路
看书
```python
class Solution:
    # matrix类型为二维列表，需要返回列表
    def printMatrix(self, matrix):
        if matrix is None:
            return []
        start = 0
        rows = len(matrix)
        cols = len(matrix[0])
        res = []
        while cols > start * 2 and rows > start * 2:
            res += self.printCircle(matrix, rows, cols, start)
            start += 1
        return res
    
    def printCircle(self, matrix, rows, cols, start):
        end_x = rows - 1 - start
        end_y = cols - 1 - start
        res = []
        # 从左到右打印一行
        for col in range(start, end_y+1):
            res.append(matrix[start][col])
        # 从上到下打印一列
        if start < end_x:
            for row in range(start+1, end_x+1):
                res.append(matrix[row][end_y])
        # 从右到左打印一行
        if start < end_x and start < end_y:
            for col in range(start, end_y)[::-1]:
                res.append(matrix[end_x][col])
        # 从下到上打印一列
        if start < end_x and start < end_y:
            for row in range(start+1, end_x)[::-1]:
                res.append(matrix[row][start])
        return res
```
