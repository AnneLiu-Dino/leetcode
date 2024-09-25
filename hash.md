#### ==242.有效的字母异位词==

多利用数组的index作为索引去操作

借用相对值 as array index

ord() 是py to get ascii code

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        record = [0]*26
        ascii_a = ord("a")
        for i in s:
            record[ord(i)-ascii_a]+=1
        for j in t:
            record[ord(j)-ascii_a]-=1    
        for r in record:
            if r >0 or r<0:
                return False
        return True

```

#### ==349. 两个数组的交集==

几个注意points:
1、数组作为hash table, 由于数值<=1000, 可以用数组，过大的话考虑set
2、使用数组，要分**清楚** 哪个是**index**
3、record1[i]>0 and record2[i]>0 可能不够优雅，范例是：record1[i]*record2[i] >0 ；<==我觉得这种方式很优雅，得学习

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        record1 = [0] * 1001
        record2 = [0] * 1001
        result = []

        for i in range(len(nums1)):
            index = nums1[i]
            record1[index] +=1
            
        for i in range(len(nums2)):
            index = nums2[i]
            record2[index] +=1

        for i in range(1001):
            if record1[i]>0 and record2[i]>0:
                result.append(i)

        return result


```
#### ==1. 两数之和==

使用字典，可以快速查找，需要清楚，key 和value分别是什么

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        dic = dict()
        
        for index, value in enumerate(nums):
            if target - value in dic:
                return [index, dic[target - value]]
            dic[value] = index
```

#### ==454. 四数相加 II==
这个题目的思路让我好惊艳
将4个array combine into 2 array，这样could directly simplify complexity。使用sum 的 反数去search hashtable。
最重要的是，hash的value，由于这个题目是要返回数量，那么value是**枚举的数量**。

```python
class Solution:
    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        table = dict()
        res = 0

        for n1 in nums1:
            for n2 in nums2:
                n_sum = n1+n2
                if n_sum in table:
                    table[n_sum] +=1
                else:
                    table[n_sum] = 1    
        
        for n3 in nums3:
            for n4 in nums4:
                n_sum = -(n3+n4)
                if n_sum in table:
                    res += table[n_sum]
        
        return res

```
#### ==383. 赎金信==
这题我完全使用了242的思路。

```python
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        arr = [0] * 26
        a_ascii = ord("a")

        for s in magazine:
            index = ord(s) - a_ascii
            arr[index] +=1
        
        for s in ransomNote:
            index = ord(s) - a_ascii
            if(arr[index]>0):
                arr[index] -=1
            else:
                return False
        return True

```
#### ==15. 三数之和==
这题确实会复杂一些，一些细节需要考虑的比较多。
首先，要对array排序，因为只要value，不需要下标
另外 如果i的value已经>0，后面的left，right的value的sum就不可能=0了
我感觉需要注意的是对于i的去重，如果和前面的值相同，说明会产生相同的结果，可直接continue

当sum>0,由于已经排序，说明需要有一个值变小，才能变成0。因此将right往左边移动
另外还需要注意left和right的去重
当结果=0时，别忘了将left和right移动，寻找下一个目标数组

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        res = []
        # 排序
        nums.sort()

        for i in range(len(nums)):
            # 无论i在哪个位置，但凡>0,后面的i，left，right都没办法sum成0，因为已经排序
            if nums[i] > 0:
                return res
            # i 的 去重
            if i > 0 and nums[i] == nums[i-1]:
                continue

            left = i + 1
            right = len(nums) -1

            while left<right:
                n_sum = nums[i]+nums[left]+nums[right]

                if n_sum == 0:
                    res.append([nums[i],nums[left],nums[right]])

                    # 防止一样的结果，要跳过
                    while left<right and nums[left] == nums[left+1]:
                        left +=1
                    while left<right and nums[right] == nums[right-1]:
                        right -=1
                    
                    left+=1
                    right-=1

                if n_sum >0:
                    right-=1
                if n_sum <0:
                    left+=1

        return res

        


```
