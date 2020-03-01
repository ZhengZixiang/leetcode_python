## 问题
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。
例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。

NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。

## 思路
1. 暴力法，从头到尾遍历到第一个小于数组头元素的即是最小数。直接min(rotateArray)
2. 二分查找。p1指向数组头，p2指向数组尾，利用二分查找法，满足p1始终是二分后前半非递减部分的头元素，p2是后半非递减部分的尾元素。需要考虑两种特殊情况：
  - 当原数组从index=0开始旋转，即旋转数组是排序数组本身。那么直接返回头元素即可
  - 当数组中存在多个重复元素，使得头尾元素与中间元素相等，无法确定中间数字是属于前半还是后半非递减子数组，只能暴力顺序查找
```python
class Solution:
    def minNumberInRotateArray(self, rotateArray):
        p1, p2 = 0, len(rotateArray) - 1
        while rotateArray[p1] >= rotateArray[p2]:
            mid = (p1 + p2) // 2
            if rotateArray[mid] == rotateArray[p1] == rotateArray[p2]:
                return min(rotateArray)
            if rotateArray[mid] > rotateArray[p1]:
                p1 = mid
            elif rotateArray[mid] < rotateArray[p2]:
                p2 = mid
            else:
                return rotateArray[p2]
        return rotateArray[0]
```
