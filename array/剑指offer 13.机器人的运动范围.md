## 问题
地上有一个m行和n列的方格。一个机器人从坐标0,0的格子开始移动，每一次只能向左，右，上，下四个方向移动一格，但是不能进入行坐标和列坐标的数位之和大于k的格子。 例如，当k为18时，机器人能够进入方格（35,37），因为3+5+3+7 = 18。但是，它不能进入方格（35,38），因为3+5+3+8 = 19。请问该机器人能够达到多少个格子？

## 思路
与剑指offer 12题一样的回溯法思想，不难，关键在于思路的清晰。题解逻辑基本与书中一致。
```python
class Solution:
    def movingCount(self, threshold, rows, cols):
        if threshold < 0 and rows < 0 and cols < 0:
            return 0
        visited = [False] * rows * cols
        return self.movingCountCore(threshold, rows, cols, 0, 0, visited)

    def movingCountCore(self, threshold, rows, cols, row, col, visited):
        count = 0
        if 0 <= row < rows and 0 <= col < cols and not visited[row * cols + col] and \
                threshold >= self.getDigitSum(row) + self.getDigitSum(col):
            visited[row * cols + col] = True
            count = 1 + \
                    self.movingCountCore(threshold, rows, cols, row + 1, col, visited) + \
                    self.movingCountCore(threshold, rows, cols, row - 1, col, visited) + \
                    self.movingCountCore(threshold, rows, cols, row, col + 1, visited) + \
                    self.movingCountCore(threshold, rows, cols, row, col - 1, visited)
        return count

    def getDigitSum(self, number):
        sum = 0
        while number > 0:
            sum += number % 10
            number //= 10
        return sum
```
