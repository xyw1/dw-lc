

#### [344. 反转字符串](https://leetcode-cn.com/problems/reverse-string/)

难度简单490

编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 `s` 的形式给出。

不要给另外的数组分配额外的空间，你必须**[原地](https://baike.baidu.com/item/原地算法)修改输入数组**、使用 O(1) 的额外空间解决这一问题。

 

**示例 1：**

```
输入：s = ["h","e","l","l","o"]
输出：["o","l","l","e","h"]
```

**示例 2：**

```
输入：s = ["H","a","n","n","a","h"]
输出：["h","a","n","n","a","H"]
```

 

**提示：**

- `1 <= s.length <= 105`

- `s[i]` 都是 [ASCII](https://baike.baidu.com/item/ASCII) 码表中的可打印字符

  

执行用时：40 ms, 在所有 Python3 提交中击败了68.65%的用户

内存消耗：19.2 MB, 在所有 Python3 提交中击败了38.93%的用户

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        left,right=0,len(s)-1
        while left<right:
            s[left],s[right]=s[right],s[left]
            left+=1
            right-=1
        return s
```



#### [5. 三数之和](https://leetcode-cn.com/problems/3sum/)

难度中等4019

给你一个包含 `n` 个整数的数组 `nums`，判断 `nums` 中是否存在三个元素 *a，b，c ，*使得 *a + b + c =* 0 ？请你找出所有和为 `0` 且不重复的三元组。

**注意：**答案中不可以包含重复的三元组。

 

**示例 1：**

```
输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]
```

**示例 2：**

```
输入：nums = []
输出：[]
```

**示例 3：**

```
输入：nums = [0]
输出：[]
```

 

**提示：**

- `0 <= nums.length <= 3000`
- `-105 <= nums[i] <= 105`



解法1:暴力搜索

结果：超出时间限制



```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        ans = []
        for first in range(n):
            for second in range(first+1,n):
                for third in range(second+1,n):
                    if first != second != third:
                        if nums[first]+nums[second]+nums[third]==0:
                            if set([nums[first],nums[second],nums[third]] ) not in map(set,ans):
                                ans.append( [nums[first],nums[second],nums[third]] )
        return ans
```



解法2: 双指针

当我们需要枚举数组中的两个元素时，如果我们发现随着第一个元素的递增，第二个元素是递减的，那么就可以使用双指针的方法，将枚举的时间复杂度从 O(N^2)减少至 O(N)。为什么是 O(N) 呢？这是因为在枚举的过程每一步中，「左指针」会向右移动一个位置（也就是题目中的 b），而「右指针」会向左移动若干个位置，这个与数组的元素有关，但我们知道它一共会移动的位置数为 O(N)，均摊下来，每次也向左移动一个位置，因此时间复杂度为 O(N)。



执行用时：612 ms, 在所有 Python3 提交中击败了79.30%的用户

内存消耗：17.5 MB, 在所有 Python3 提交中击败了72.30%的用户

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums = sorted(nums)
        n = len(nums)
        ans = []
        for first in range(n):
          	third=n-1 # third=n-1必须写在第一个循环里，写在第二个循环里不是双指针
            if first==0 or nums[first]!=nums[first-1]:
                target = -nums[first]
                for second in range(first+1,n):
                    if second ==first+1 or nums[second]!=nums[second-1]:
                        while second < third and nums[second] + nums[third] > target:
                            third -= 1
                            #if third==n-1 or nums[third]!=nums[third+1]:
                        if second == third:
                            break
                        if  nums[second]+nums[third]==target:
                            ans.append( [nums[first],nums[second],nums[third]] )

        return ans
```


