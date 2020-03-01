## 问题
请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一个格子开始，每一步可以在矩阵中向左，向右，向上，向下移动一个格子。如果一条路径经过了矩阵中的某一个格子，则该路径不能再进入该格子。

## 思路
回溯法，用visited判断路径是否走过，若走过或者越界或者不能构成字符串则回退一步。代码逻辑和书中一致。
```python
# -*- coding:utf-8 -*-
class Solution:
    def hasPath(self, matrix, rows, cols, path):
        if matrix is None or rows < 1 or cols < 1 or path is None:
            return False
        visited = [False] * rows * cols
        for i in range(rows):
            for j in range(cols):
                if self.hasPathCore(matrix, rows, cols, i, j, path, 0, visited):
                    return True
        return False

    def hasPathCore(self, matrix, rows, cols, row, col, string, pathLength, visited):
        if pathLength >= len(string):
            return True
        hasPath = False
        if 0 <= row < rows and 0 <= col < cols and \
                matrix[row * cols + col] == string[pathLength] and not visited[row * cols + col]:
            pathLength += 1
            visited[row * cols + col] = True
            hasPath = self.hasPathCore(matrix, rows, cols, row + 1, col, string, pathLength, visited) or \
                self.hasPathCore(matrix, rows, cols, row - 1, col, string, pathLength, visited) or \
                self.hasPathCore(matrix, rows, cols, row, col + 1, string, pathLength, visited) or \
                self.hasPathCore(matrix, rows, cols, row, col - 1, string, pathLength, visited)
            if not hasPath:
                pathLength -= 1
                visited[row * cols + col] = False
        return hasPath
```
