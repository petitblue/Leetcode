## 203. Remove Linked List Elements
https://leetcode.com/problems/remove-linked-list-elements/description/
```sh
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        if head !=None and head.val == val:
            head = head.next
        curr = head
        while curr.next:
            if curr.next.val == val:
                curr.next = curr.next.next
            else:
                curr = curr.next
        return head
 ```
 Tow pointer and Dummy node
 -dummy node will help to deal with the head node
 - prev and curr pointer make easier to realize the deletion
 
 ```sh
 class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        dummy = ListNode()
        dummy.next = head
        curr = head
        prev = dummy
        # prev curr next.                   prev    next
        # 1.    2.   3    after delete 2.    1.        3 no need to move   prev, but curr move to next 
        #  if curr.val is not the target, both prev and curr move to next position.                             
        while ( curr != None): 
            if curr.val == val:
                prev.next = curr.next
                curr = curr.next
            else:
                prev = prev.next
                curr = curr.next
            
        
        return dummy.next
   ```
   
 707.Design linked list
 
 ```sh
 typedef struct slist {
   int data;
   struct slist* next;
   int size;
    
} MyLinkedList;

MyLinkedList* myLinkedListCreate() {
    MyLinkedList* head = (MyLinkedList*)malloc(sizeof(MyLinkedList));
    head->next = NULL;
    head->size = 0;
    return head;
}

int myLinkedListGet(MyLinkedList* obj, int index) {
  if(obj == NULL){
      return -1;
  }
  if(index > obj->size-1 || index <0){
      return -1;
  }
  MyLinkedList* curr = obj->next; // head is null, like a dummy head.
  int count =0;
  while(curr!=NULL){
      if(count == index){
          return curr->data;
      }
      curr = curr->next;
      count ++;
  }
  return -1;
  
}

void myLinkedListAddAtHead(MyLinkedList* obj, int val) {
  if(obj == NULL){
      return;
  } // obj ->(obj->next)
  // obj-> newNode ->(obj->next)
  MyLinkedList* newNode= (MyLinkedList*)malloc(sizeof(MyLinkedList));
  newNode->data = val;
  newNode->next = obj->next;
  obj->next = newNode;
  obj->size ++;
}

void myLinkedListAddAtTail(MyLinkedList* obj, int val) {
  if(obj == NULL){
      return;
  }
  MyLinkedList* newNode= (MyLinkedList*)malloc(sizeof(MyLinkedList));
  if(newNode != NULL) {
      // if obj->size = 0. obj ->NULL
      // obj->newNode->NULL 
      // if obj->size >0  iterate the list. obj->a -> ... tail ->NULL
    obj->size ++;
    newNode->data = val;
    if(obj->size == 0){
        newNode->next = obj->next;
        obj->next = newNode;
        
  } else{
       MyLinkedList* curr = obj->next;
       for(int i = 1; curr->next != NULL; i++) {
           curr = curr->next; // iterate to the tail of the list 
           // if is curr !=NULL, then in the end curr will point to NULL
       }
       curr->next = newNode;
        newNode->next = NULL;
  }
  
  
  
  }
}
// add before the index
void myLinkedListAddAtIndex(MyLinkedList* obj, int index, int val) {
  if(obj == NULL){
      return;
  }
  
  if(index<0 || index > obj->size-1){
      return;
  }
  
   MyLinkedList* curr = obj->next;
   for(int i = 1; curr!=NULL; i++) {
      if(i == index) {
        MyLinkedList* newNode= (MyLinkedList* )malloc(sizeof(MyLinkedList));
        newNode->data = val;
        newNode->next = curr->next;
        curr->next = newNode;
       
      }
      curr = curr->next;
      
  }
  obj->size ++;
  
}

void myLinkedListDeleteAtIndex(MyLinkedList* obj, int index) {
  if(index ==0){ // delete the first element
      MyLinkedList*  tmp = obj->next;
      // obj->(obj->next)-> (obj->next->next)
      //       tmp            tmp->next
      if(tmp != NULL) {
          obj->next = tmp->next;
          free(tmp);
      }
  }
  MyLinkedList* curr = obj->next;
  for(int i = 1; curr!=NULL && curr->next != NULL ; i++) {
      if(i==index-1) {
          curr->next = curr->next->next;
      }
      curr = curr->next;
  }
}

void myLinkedListFree(MyLinkedList* obj) {
    MyLinkedList*  curr = obj->next;
    //obj -> curr -> (curr->next)->(curr->next->next)
    while(curr->next!= NULL) {
        MyLinkedList*  temp = curr->next;
        curr->next = curr->next->next;
        free(temp);
    }
    free(obj);
    
    
}

```
206. Reverse Linked List

https://leetcode.com/problems/reverse-linked-list/
 ```sh

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* reverseList(struct ListNode* head){
  struct  ListNode* prev =NULL;
  
  struct  ListNode* curr = head;
  struct  ListNode* next = NULL;
  // null -> 1 -> 2->3 -> NULL
  // prev.  curr  next
  while(curr != NULL) {
      next = curr->next;
      curr->next = prev; // // null <-1     2->3 -> NULL
      prev = curr;           //       prev 
      curr = next;           //             curr
  }
  return prev;

}
 ```

