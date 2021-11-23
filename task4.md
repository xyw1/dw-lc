#### [704. 二分查找](https://leetcode-cn.com/problems/binary-search/)



给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。


示例 1:

```
输入: nums = [-1,0,3,5,9,12], target = 9
输出: 4
解释: 9 出现在 nums 中并且下标为 4
```


示例 2:

```
输入: nums = [-1,0,3,5,9,12], target = 2
输出: -1
解释: 2 不存在 nums 中因此返回 -1
```


提示：

1. 你可以假设 nums 中的所有元素是不重复的。
2. n 将在 [1, 10000]之间。
3. nums 的每个元素都将在 [-9999, 9999]之间。

解法1:

执行用时：52 ms, 在所有 Python3 提交中击败了7.77%的用户

内存消耗：16 MB, 在所有 Python3 提交中击败了5.47%的用户

```python
class Solution:
    def search(self, nums,target) : 
        def is_in(L,left,right,x):
            l = L[left:right]
            if x < l[0]:
                return False
            elif x > l[-1]:
                return False
            else:
                return True
        index = -1
        left, right = 0,len(nums)
        if is_in(nums,left,right,target):
            while True:
                if left==(right-1):
                    index=left
                    break
                mid = ceil((left+right)/2)
                if is_in(nums,left,mid,target):
                    right = mid
                elif is_in(nums,mid,right,target):
                    left = mid
                else:
                    index=-1
                    break
        else:
            index = -1
        return index
            
```





#### [69. Sqrt(x)](https://leetcode-cn.com/problems/sqrtx/)

给你一个非负整数 `x` ，计算并返回 `x` 的 **算术平方根** 。

由于返回类型是整数，结果只保留 **整数部分** ，小数部分将被 **舍去 。**

**注意：**不允许使用任何内置指数函数和算符，例如 `pow(x, 0.5)` 或者 `x ** 0.5` 。

 

**示例 1：**

```
输入：x = 4
输出：2
```

**示例 2：**

```
输入：x = 8
输出：2
解释：8 的算术平方根是 2.82842..., 由于返回类型是整数，小数部分将被舍去。
```

 

**提示：**

- `0 <= x <= 231 - 1`

解法1: 袖珍计算器算法

执行用时：80 ms, 在所有 Python3 提交中击败了13.07%的用户

内存消耗：32.1 MB, 在所有 Python3 提交中击败了5.50%的用户

```python
class Solution:
    def mySqrt(self, x: int) -> int:
        if x==0:
            return 0
        else:
            n = int(e**(0.5*log(x)))
        return n+1 if (n+1)**2 <= x else n
```

解法2: 二分查找

执行用时：32 ms, 在所有 Python3 提交中击败了90.02%的用户

内存消耗：14.7 MB, 在所有 Python3 提交中击败了99.02%的用户

```python
class Solution:
    def mySqrt(self, x: int) -> int:
        left, right = 0, x
        n = -1
        while left <= right:
            mid = int((left+right)/2)
            if mid**2<=x:
                left = mid+1
                n = mid
            else:
                right = mid-1
        return n
```

总结：在一个顺序的序列中查找一个最大的满足某条件的值也可以使用二分查找