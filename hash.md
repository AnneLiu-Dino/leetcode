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