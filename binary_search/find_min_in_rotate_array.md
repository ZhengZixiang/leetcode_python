# 问题
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。 输入一个有序的数组的一个旋转，输出旋转数组的最小元素。 例如数组[3,4,5,1,2]为[1,2,3,4,5]的一个旋转，该数组的最小值为1。 NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。

# 思路
- 暴力遍历，当遇到某个数小于前面的数时，显然他就是最小元素。时间复杂度O(N)。

- 二分查找，设置两个游标分别指向数组首尾。
二分查找根据指针移动方式的不同，会有两种解。最直觉的二分思路会有个问题，如[1,0,1,1,1]，最后会返回1，此时只能顺序查找。
```python
def find_min(arr):
  if len(arr) == 0:
    return 0
  low = 0
  high = len(arr) - 1
  while high - low > 1:
    if arr[mid] == arr[low] and arr[low] == arr[high]:
      for i in range(low+1, high+1):
        if arr[i] < arr[low]:
          return arr[i]
    elif arr[mid] >= arr[low]:
      low = mid
    elif arr[mid] <= arr[high]:
      high = mid
  return arr[high]
```

一个小小的改进如下
```python
def find_min(arr):
  if len(arr) == 0:
    return 0
  low = 0
  high = len(arr) - 1
  while low < high:
    mid = (low + high) >> 1
    if arr[mid] > arr[right]:
      low = mid + 1
    elif arr[mid] < arr[high]:
      high = mid
    else:
      high -= 1
  return arr[low]
```
