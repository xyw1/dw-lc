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

