# Intersection of Two Linked Lists

**Example 1:**

[![](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)

```text
Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3Output: Reference of the node with value = 8Input Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,0,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
```

**Example 2:**

[![](https://assets.leetcode.com/uploads/2018/12/13/160_example_2.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_2.png)

```text
Input: intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1Output: Reference of the node with value = 2Input Explanation: The intersected node's value is 2 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [0,9,1,2,4]. From the head of B, it reads as [3,2,4]. There are 3 nodes before the intersected node in A; There are 1 node before the intersected node in B.
```

**Example 3:**

[![](https://assets.leetcode.com/uploads/2018/12/13/160_example_3.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_3.png)

```text
Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2Output: nullInput Explanation: From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.Explanation: The two lists do not intersect, so return null.
```

```text
# Definition for singly-linked list.# class ListNode(object):#     def __init__(self, x):#         self.val = x#         self.next = Noneclass Solution(object):    def getIntersectionNode(self, headA, headB):        """        :type head1, head1: ListNode        :rtype: ListNode        """#         if not headA or not headB:#             return None#         endB = headB#         while endB.next:#             endB = endB.next#         endB.next = headB#         slow = quick = headA#         while quick and quick.next:#             slow = slow.next#             quick = quick.next.next#             if slow == quick:#                 break#         if not quick or not quick.next:#             endB.next = None#             return None#         slow = headA#         while slow and slow != quick:#             slow = slow.next#             quick = quick.next#         endB.next = None#         return slow        pa, pb = headA, headB        while pa != pb:            pa = headB if not pa else pa.next            pb = headA if not pb else pb.next        return pa
```

