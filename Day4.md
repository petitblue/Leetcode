##24. 两两交换链表中的节点 

https://leetcode.com/problems/swap-nodes-in-pairs/
-set up a dummy head
-before swap, store the node
-decide when the while loop will stop


```sh
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # dummy - 1- 2 -3 - 4 - None
        # prev.  curr next
        # after swap 1 and 2 :
        # dummy - 2  -1   -3 -4- None
        #          prev.curr next
        # after swap 3, 4 : 
        #  dummy - 2 -1 -4 -3 -None
        #                 prev.curr next
        # if the number of element is odd, we won't swap the last element, then stop
        #  dummy  - 1- 2 -3 - 4 - 5 -None
        #                    prev.curr next
        
        if not head:
            return None
        dummy = ListNode(next = head)
        
        prev = dummy
        curr = head
        while curr!= None and curr.next != None :  # when we have a pair to swap
            # store node
            temp1 = curr
            temp2 = curr.next.next
            # swap node
            prev.next = curr.next
            curr.next.next = temp1
            temp1.next = temp2
            # move prev and curr
            prev = prev.next.next  # afte swap, prev pointer moves two steps
            curr = prev.next
        return dummy.next
        
  ```


##19. Remove Nth Node From End of List
https://leetcode.com/problems/remove-nth-node-from-end-of-list/

Two pointer && dummy node
-use dummy node so it's easier to delete the head node
- dummy - 1 - 2 -3 - 4 - None.  delete 2nd node from the end 3
-               left      right
- to find out the node to delete, we will make the right pointer point to None, and right-left+1  = n
- however to the notice, if we will delete the node 3, we will need the pointer before the node 3
- one way is the right pointer move 1 more step, or the left pointer one step back
```sh

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0,head)
        left = dummy
        right = head
        # make right and left's distance is n
        while n> 0 and right != None:
            right = right.next
            n -= 1
        # right pointer move to the none ,
        while left!= None and right != None:
            left = left.next
            right = right.next
        #delete the ListNode
        if left and left.next:
          left.next = left.next.next

        return dummy.next
```
