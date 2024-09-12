#### ==704 binary search==

**区间定义需要明确：[1,1] or [1,2) **

**当区间定义为[]时，对left, right的赋值应该不包含mid的。left, right的赋值与while中的condition是挂钩的。**

```python
class Solution:
    def search(self, arr: List[int], target: int) -> int:
        left = 0
        right = len(arr) -1
        while(left<=right):
            mid = (left+right)//2
            if(arr[mid] == target):
                return mid
            if(target<arr[mid]):
                right = mid -1
            if(target>arr[mid]):
                left = mid + 1
        return -1
        

```
#### ==27 remove-element==

**as we know, 数组是存放在连续内存空间上的相同类型数据的集合。数组中元素的删减，会使得后面的元素往前覆盖，therefore, no deletion but replacement；并用size对确定数组长度 **

快指针：探索需要使用的value
慢指针：使用快指针的value去形成最终的array

当fast与target值相同时，fast往后走（ignore the value of target); Instead，slow使用fast的值

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        slow = 0
        for fast in range(len(nums)):
            if(nums[fast]!=val):
                nums[slow] = nums[fast]
                slow+=1
        return slow
        

```

#### ==977 squares-of-a-sorted-array==

双指针这个思路蛮有意思的，在用abs绝对值去判断。

while中的condition 也可以是：arr_index >= 0

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        arr = [0] * len(nums)
        left = 0
        right = len(nums) - 1
        arr_index = len(nums) - 1

        while(left <= right):
            if(abs(nums[left])<=abs(nums[right])):
                arr[arr_index] = nums[right] ** 2
                right-=1
            else:
                arr[arr_index] = nums[left]**2
                left+=1
            
            arr_index-=1
        return arr    




```

#### ==209.长度最小的子数组==

原本想用快慢指针去控制这个搜索窗口，但是需要用到if；但显然if无法满足持续往后移动的需求。
**学到了while的使用**


```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        min_size = math.inf
        total = 0
        flag = 0

        for i in range(len(nums)):
            total += nums[i]
            while(total>=target):
                min_size = min(min_size, i - flag + 1)
                total -= nums[flag]
                flag += 1
        
        return 0 if min_size == math.inf else min_size

```

#### ==59.spiral-matrix-ii==

这道题要多一点耐心，按照卡尔的思路，得写个运行规律，才能把代码盘出来。

我觉得关键点是每一圈x,y的值与offset的关系分析明白，就能手搓出来。


![image-20240913091027880](/Users/liuyan/Master/leetcode/array.assets/image-20240913091027880.png)


```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        matrix = [[0] * n for _ in range(n)]
        start_x, start_y = 0,0
        cycle = n // 2
        count = 1

        for offset in range(1, cycle+1):
            for y in range(start_y, n-offset):
                matrix[start_x][y] = count
                count +=1
            for x in range(start_x, n-offset):
                matrix[x][n-offset] = count
                count +=1
            for y in range(n-offset, offset -1, -1):
                matrix[n-offset][y] = count
                count +=1
            for x in range(n-offset,offset -1, -1):
                matrix[x][start_y] = count
                count +=1
            start_x += 1
            start_y += 1
        
        if(n%2 !=0):
            mid = n//2
            matrix[mid][mid] = count
        
        return matrix
```
#### ==前缀和==
思路很妙啊，把每一步累加保存下来。
