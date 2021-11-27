

# 未归类

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

# 

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
    def sortArray(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        return sorted(nums,revered=True)[k-1]
```

# 归并排序

#### [912. 排序数组](https://leetcode-cn.com/problems/sort-an-array/)

给你一个整数数组 nums，请你将该数组升序排列。



示例 1：

```
输入：nums = [5,2,3,1]
输出：[1,2,3,5]
```


示例 2：

```
输入：nums = [5,1,1,2,0,0]
输出0,0,1,1,2,5]
```


提示：

`1 <= nums.length <= 50000`
`-50000 <= nums[i] <= 50000`



解法1:

执行用时：28 ms, 在所有 Python 提交中击败了100.00%的用户

内存消耗：20.8 MB, 在所有 Python 提交中击败了69.15%的用户

```python
class Solution(object):
    def sortArray(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        return sorted(nums)
```



解法2:

执行用时：372 ms, 在所有 Python 提交中击败了38.59%的用户

内存消耗：22.1 MB, 在所有 Python 提交中击败了9.83%的用户

```python
class Solution(object):
    def sortArray(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        def sort(nums):
            if len(nums)==1:
                return nums
            n = len(nums)/2
            part1 = nums[:n]
            part2 = nums[n:]
            return merge(sort(part1),sort(part2))
           
        def merge(L1,L2):
            i = 0
            j = 0
            L = []
            while True:
                if L1[i]<L2[j]:
                    L.append(L1[i])
                    i+=1
                elif L1[i]>L2[j]:
                    L.append(L2[j])
                    j+=1
                elif L1[i]==L2[j]:
                    L.append(L1[i])
                    L.append(L2[j])
                    i+=1
                    j+=1
                if not(i<len(L1) and j<len(L2)):
                    if i==len(L1):
                        L+=L2[j:]
                    if j==len(L2):
                        L+=L1[i:]
                    break
            return L
        return sort(nums)
```



解法3:

执行用时：6528 ms, 在所有 Python 提交中击败了5.06%的用户

内存消耗：21.6 MB, 在所有 Python 提交中击败了19.85%的用户



```python
class Solution(object):
    def sortArray(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        def sort(nums):
            if len(nums)==1:
                return nums
            n = len(nums)/2
            part1 = nums[:n]
            part2 = nums[n:]
            return merge(sort(part1),sort(part2))
           
        def merge(L1,L2):
            L = []
            while L1!=[] and L2!=[]:
                if L1[0]<L2[0]:
                    L.append(L1[0])
                    L1.pop(0)
                elif L1[0]>L2[0]:
                    L.append(L2[0])
                    L2.pop(0)
                elif L1[0]==L2[0]:
                    L.append(L1[0])
                    L.append(L2[0])
                    L1.pop(0)
                    L2.pop(0)
                
            if L1==[]:
                L+=L2
            if L2==[]:
                L+=L1
            return L
        return sort(nums)
```



# 快速排序

in-place partition

1. left为最左，right为最右，patition_index=left
2. 把pivot元素放到最末尾
3. 从最左边的元素开始：
   1. 如果元素比pivot小：
      1. 交换patition_index和当前元素的值
      2. patition_index+=1
4. 交换patition_index和right(pivot的暂存位置)

![](/Users/yunwanxu/git/dw-lc/quick_sort_partition.gif)

#### [912. 排序数组](https://leetcode-cn.com/problems/sort-an-array/)

给你一个整数数组 nums，请你将该数组升序排列。



示例 1：

```
输入：nums = [5,2,3,1]
输出：[1,2,3,5]
```


示例 2：

```
输入：nums = [5,1,1,2,0,0]
输出0,0,1,1,2,5]
```


提示：

`1 <= nums.length <= 50000`
`-50000 <= nums[i] <= 50000`



解法1：

执行用时：596 ms, 在所有 Python 提交中击败了11.13%的用户

内存消耗：21.3 MB, 在所有 Python 提交中击败了30.12%的用户

```python
class Solution(object):
    def sortArray(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        from random import randint
        def sort(L,left,right):
            if right-left<1:
                return 
            else:
                pivot_index = randint(left,right)
                patition_index = partition(L,left,right,pivot_index)
                sort(L,left,patition_index-1)
                sort(L,patition_index,right)
                return 

        def swap(L,i,j):
                tmp = L[i]
                L[i] = L[j]
                L[j] = tmp

        def partition(L,left,right,pivot_index):
                patition_index   = left
                swap(L,pivot_index,right)
                pivot = L[right]
                for i in range(left,right):
                    if L[i]<=pivot:         
                        swap(L,patition_index,i)
                        patition_index+=1
                swap(L,patition_index,right)
                return patition_index

        sort(nums,0,len(nums)-1)
        return nums
    
```



# 计数排序



#### [912. 排序数组](https://leetcode-cn.com/problems/sort-an-array/)

给你一个整数数组 nums，请你将该数组升序排列。



示例 1：

```
输入：nums = [5,2,3,1]
输出：[1,2,3,5]
```


示例 2：

```
输入：nums = [5,1,1,2,0,0]
输出0,0,1,1,2,5]
```


提示：

`1 <= nums.length <= 50000`
`-50000 <= nums[i] <= 50000`

解法1:

执行用时：120 ms, 在所有 Python 提交中击败了88.70%的用户

内存消耗：21.7 MB, 在所有 Python 提交中击败了18.54%的用户

```python
class Solution(object):
    def sortArray(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        max_= max(nums)
        min_ = min(nums)
        n = max_ - min_ + 1 
        L = [0]*n
        for x in nums:
            L[x-min_]+=1
        new_nums = []
        for i,x in enumerate(L):
            new_nums+=[min_+i]*x
        return new_nums
```





# 桶排序

#### [912. 排序数组](https://leetcode-cn.com/problems/sort-an-array/)

给你一个整数数组 nums，请你将该数组升序排列。



示例 1：

```
输入：nums = [5,2,3,1]
输出：[1,2,3,5]
```


示例 2：

```
输入：nums = [5,1,1,2,0,0]
输出0,0,1,1,2,5]
```


提示：

`1 <= nums.length <= 50000`
`-50000 <= nums[i] <= 50000`

解法1:

执行用时：68 ms, 在所有 Python3 提交中击败了91.46%的用户

内存消耗：21.3 MB, 在所有 Python3 提交中击败了30.88%的用户

```python
class Solution(object):
    def sortArray(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        from math import ceil
        max_= max(nums)
        min_ = min(nums)
        n = max_ - min_ + 1 
        if len(nums)<=1:
            return nums
        bin_size = ceil(n/10)
        bin_n = ceil(n/bin_size)
        bucket = {i:[] for i in range(bin_n)}
        
        for x in  nums:
            bucket[int((x-min_)/bin_size)].append(x)

        return [x for i in range(bin_n) for x in sorted(bucket[i])]
```



# 基数排序

#### [912. 排序数组](https://leetcode-cn.com/problems/sort-an-array/)

给你一个整数数组 nums，请你将该数组升序排列。



示例 1：

```
输入：nums = [5,2,3,1]
输出：[1,2,3,5]
```


示例 2：

```
输入：nums = [5,1,1,2,0,0]
输出0,0,1,1,2,5]
```


提示：

`1 <= nums.length <= 50000`
`-50000 <= nums[i] <= 50000`



解法1:	

执行用时：408 ms, 在所有 Python3 提交中击败了51.35%的用户

内存消耗：39 MB, 在所有 Python3 提交中击败了5.02%的用户

```python
class Solution(object):
    def sortArray(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        import numpy as np
        pos = [x for x in nums if x>=0]
        neg = [x for x in nums if x<0]
        
        def radix_sort(L,max_digit):
            for digit in range(max_digit):
                if len(L)<=1:
                    return L
                
                radix = {i:[] for i in range(10)}
                for x in L:
                    index = int(str(x).zfill(max_digit)[-digit-1])
                    radix[index].append(x)

                L = [x for i in range(10) for x in radix[i]]
            return L

        if len(pos)<=1:
            pass
        else:
            max_digit = int(np.log10(max(pos)))+1
            pos = radix_sort(pos,max_digit)
        if len(neg)<=1:
            pass
        else:
            neg = [abs(x) for x in neg]
            max_digit = int(np.log10(max(neg)))+1
            neg = radix_sort(neg,max_digit)
            neg = [-1*x for x in reversed(neg)]
        return neg+pos
```

