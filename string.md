#### ==344. 反转字符串==
双指针O(n)秒了
s.reserve()

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        left = 0
        right = len(s)-1
        while left < right:
            # temp = s[left]
            # s[left] = s[right]
            # s[right] = temp
            s[left], s[right] = s[right], s[left]

            left +=1
            right -=1
           
```
#### ==541. 反转字符串 II==
这题我觉得看明白题目很关键。
还有range的使用，直接用[i:i+k]左闭右开 去截取要反转的string

```python
class Solution:
    def reverseStr(self, s: str, k: int) -> str:

        def reverse_str(s):
            left = 0
            right = len(s)-1
            while left<right:
                s[left], s[right] = s[right], s[left]
                left+=1
                right-=1
            return s

        res = list(s)
        for cur in range(0, len(s), 2*k):
            reversed_s = reverse_str(res[cur: cur+k])
            res[cur: cur+k] = reversed_s
            print(cur)

        return "".join(res)
           
```
