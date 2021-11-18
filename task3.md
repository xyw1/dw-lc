



####  [剑指 Offer 45. 把数组排成最小的数](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

示例 1:

```txt
输入: [10,2]
输出: "102"
```


示例 2:

```
输入: [3,30,34,5,9]
输出: "3033459"
```


提示:

- 0 < nums.length <= 100

说明:

- 输出结果可能非常大，所以你需要返回一个字符串而不是整数
- 拼接起来的数字可能会有前导 0，最后结果不需要去掉前导 0

```python
class Solution(object):
    def minNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: str
        """
        def less_than(x,y):
            if int(str(x)+str(y))<int(str(y)+str(x)):
                return True
            else:
                return False
        def get_min_index(L):
            min_i = 0
            for i,x in enumerate(L):
                if less_than(x,L[min_i]):
                    min_i = i
            return min_i
        string = ''
        n = len(nums)
        for i in range(n):
            idx = get_min_index(nums)
            string+=str(nums.pop(idx))
        return string
```



#### [283. 移动零](https://leetcode-cn.com/problems/move-zeroes/)

给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

示例:

```txt
输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
```

**说明**:

1. 必须在原数组上操作，不能拷贝额外的数组。
2. 尽量减少操作次数。



解法1:

```python
class Solution(object):
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        for i in range(n):
            try:
                idx = nums.index(0)
                nums.pop(idx)
                nums.append(0)
            except ValueError:
                break
        return nums
```



解法2:

```python
class Solution(object):
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        n = nums.count(0)
        for i in range(n):
            nums.remove(0)
            nums.append(0)
        return nums
```



#### [215. 数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

请注意，你需要找的是数组排序后的第 `k` 个最大的元素，而不是第 `k` 个不同的元素。

**示例 1:**

```txt
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
```

**示例 2:**

```txt
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```

**提示：**

- `1 <= k <= nums.length <= 104`
- `-104 <= nums[i] <= 104`

```python
class Solution(object):
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        return sorted(nums,reverse=True)[k-1]
```

