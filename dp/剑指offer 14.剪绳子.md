## 问题
给你一根长度为n的绳子，请把绳子剪成整数长的m段（m、n都是整数，n>1并且m>1），每段绳子的长度记为k[0],k[1],...,k[m]。请问k[0]xk[1]x...xk[m]可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

## 思路
长度小于3的时候做特殊的判断，而大于3的时候，这里有一个特殊的条件，也就是dp=[0, 1, 2, 3]，许多书和博客题解都没有提到为什么dp初始是这样，这是当绳子剪到2或3时无需再剪，而且实际上当长度大于3时，乘积最大值都能由2和3表示，存在数学推导，这里就不列出来了。
1. 动态规划
```python
class Solution:
    def cutRope(self, number):
        if number < 2:
            return 0
        if number == 2:
            return 1
        if number == 3:
            return 2
        dp = [0, 1, 2, 3]
        for i in range(4, number+1):
            max = 0
            for j in range(1, i//2 + 1):
                product = dp[j] * dp[i - j]
                if product > max:
                    max = product
            dp.append(max)
        return dp[number]
```
2. 前面提到了n>3时都由2和3相乘，所以有一个快捷解，就是尽可能地找3的倍数，再尽可能地找2的倍数，当整数3余数为1时，抽一个3出来变为2*2。上述是贪心的思维，代码如下。
```python
class Solution:
    def cutRope(self, number):
        if number < 2:
            return 0
        if number == 2:
            return 1
        if number == 3:
            return 2
        mod = number % 3
        power = number // 3
        if mod == 0:
            return pow(3, power)
        elif mod == 1:
            return 2 * 2 * pow(3, power-1)
        else:
            return 2 * pow(3, power)
```
书中写法如下
```python
class Solution:
    def cutRope(self, number):
        if number < 2:
            return 0
        if number == 2:
            return 1
        if number == 3:
            return 2
        
        timesOf3 = number // 3
        if number - timesOf3 * 3 == 1:
            timesOf3 -= 1
            
        timesOf2 = (number - timesOf3 * 3) // 2
        return pow(3, timesOf3) * pow(2, timesOf2)
```
