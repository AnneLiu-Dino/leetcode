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
#### ==24. 两两交换链表中的节点==

**本来计划使用3个指针，但是无法实现，看了卡尔的讲解，原来是需要暂存4个节点，代码中node1，2，3这样再去写代码，思路会非常清晰**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy_node = ListNode(next = head)
        cur = dummy_node

        while(cur.next and cur.next.next):
            node1 = cur.next
            node2 = node1.next
            node3 = node2.next

            cur.next = node2
            node2.next = node1
            node1.next = node3

            cur = node1
        
        return dummy_node.next

```