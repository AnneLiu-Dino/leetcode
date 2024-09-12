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