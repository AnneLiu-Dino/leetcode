#### ==203.移除链表元素==

**while的终止条件是非节点，用point作为遍历的元素，探查到point下一个元素如果match target，就跳过**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        # creating dummy head, in this way, we dont need to extraly process deleting head node
        dummy_head = ListNode(next = head)
        pointer = dummy_head
        while(pointer.next):
            if(pointer.next.val == val):
                pointer.next = pointer.next.next
            else:
                pointer = pointer.next
        return dummy_head.next

```

#### ==206.reverse-linked-list==

**头开始就想到了快慢指针的解法，但没想到使用temp，不够熟练**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        point_fast = head
        point_slow = None

        while(point_fast):
            temp = point_fast.next
            point_fast.next = point_slow
            point_slow = point_fast
            point_fast = temp
        return point_slow

```
