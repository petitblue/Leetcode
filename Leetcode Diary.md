# Day 1. 
## 704 [Binary Search(https://leetcode.com/problems/binary-search/)] (https://leetcode.com/problems/binary-search/)
二分查找几个要点：
- 数组是否有序
- 确定 mid 
- 左闭右闭 /  左闭右开

```
int search(int* nums, int numsSize, int target){
   int left = 0;
   int right = numsSize-1;
   // 2,3, 4,6 target =4  mid = 3/2 =1

   while(left <= right) {
       int mid = left + (right-left)/2;
       if(nums[mid]>target) {
           right = mid - 1;
       }else if (nums[mid] <target) {
           left = mid + 1;
       }else {
           return mid;
       }
   }
   return -1;
}
```
需要注意的是mid 不要写成 (left+right)/2  if right is close to MAXINT, then left+right will create an overflow
## 27. [Remove Element(https://leetcode.com/problems/remove-element/description/)] (https://leetcode.com/problems/remove-element/description/)
### Brute force
- in the first loop, we iterate the array nums, and check each element if it equals to val. Remember that, 
  the size of the array will change when an element is deleted.
- if nums[i] == val, in the second loop, we move the i+1 and the following elements 1 place forward
   1 2 3 6 8. target =2 i =1
   1 3 6 8
 -  remember that after remove the element, i backward one place, i--
 - when the last element equals to the target, we don't remove it, we just update the numsSize. 
   
### Code
```
int removeElement(int* nums, int numsSize, int val){
    if(nums == NULL) {
        return -1;
    }
    
    for(int i = 0; i < numsSize; i++) {
        if(nums[i]==val) {
          for(int j = i; j < numsSize-1; j++){
            nums[j] = nums[j+1];
            
          }
          i--;
          numsSize--;
          
        }
        
        
    }
    
    return numsSize;
}
```
Time complexity is O(n*n) 
### Two pointer
 1   1  2 3 6 2 8. target =2 
 slow
 fast
 1   1  3 6 2 8
        slow
        fast
 fast move each time to iterate the array, nums[slow] store value except target value
 if the target is found, fast++
 if not, nums[slow] = nums [fast]
 ```
 int removeElement(int* nums, int numsSize, int val){
   int ans = numsSize;
   if(nums == NULL) {
       return -1;
   }
   int slow = 0;
   int fast;
   for(fast =0; fast < numsSize; fast++) {
      if(nums[fast] != val) {
          nums[slow]= nums[fast];
          slow++;
      }

   }
   return slow;
}
```
Time complexity is Big O(n)
