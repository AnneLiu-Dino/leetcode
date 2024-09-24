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
#### ==19.删除链表倒数第N个节点==

**看了卡尔的思路讲解后，就能把代码写出来啦，对于fast先后，然后在fast、slow同步走，真的有意思，这样就能很好的控制到要删除的节点。另外，sample code中用for循环去控制fast先走的步骤比我写的while更清晰。**

```python
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy_node = ListNode(next = head)
        fast = dummy_node
        slow = dummy_node
        while(n>=0):
            fast = fast.next
            n-=1
        #for i in range(n+1):
        #    fast = fast.next
        while(fast):
            fast = fast.next
            slow = slow.next
        slow.next = slow.next.next
        return dummy_node.next
```