#### [01.07. 旋转矩阵](https://leetcode-cn.com/problems/rotate-matrix-lcci/)

```python
class Solution(object):
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: None Do not return anything, modify matrix in-place instead.
        """
        matrix[: ] = map(list, zip(*reversed(matrix)))

```



#### [01.08. 零矩阵](https://leetcode-cn.com/problems/zero-matrix-lcci/)

```python
class Solution(object):
    def setZeroes(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: None Do not return anything, modify matrix in-place instead.
        """
        row = []
        col = []
        for i in range(len(matrix)):
            if matrix[i].count(0)!=0:
                row.append(i)
                for j in range(len(matrix[i])):
                    if matrix[i][j]==0:
                        col.append(j)
        for i in set(row):
            matrix[i]=[0]*len(matrix[i])
        for j in set(col):
            for i in range(len(matrix)):
                matrix[i][j]=0
```





#### [498. 对角线遍历](https://leetcode-cn.com/problems/diagonal-traverse/)

```python
class Solution(object):
    def findDiagonalOrder(self, mat):
        """
        :type mat: List[List[int]]
        :rtype: List[int]
        """
        m = len(mat)
        if m==0:
            return []
        else:
            n = len(mat[0])
        L = []
        for i in range(max(2*m-1,2*n-1)):
            if i%2==0:
                for j in range(max(i-m+1,0), min(i+1,n)):
                    L.append(mat[i-j][j])
            else:
                for j in reversed(range(max(i-m+1,0), min(i+1,n))):
                    L.append(mat[i-j][j])
        return L
```

