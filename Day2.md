## 977.有序数组的平方 
https://leetcode.com/problems/squares-of-a-sorted-array/description/


```sh
**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* sortedSquares(int* nums, int numsSize, int* returnSize){
   int* arr = (int*)malloc(sizeof(int)*numsSize);
   int left = 0;
   int right = numsSize -1;
   int k = numsSize -1; // index of the last element of the new arr
   *returnSize =numsSize;
   while(left<=right&& k>=0) { // remember that k has to be in bound
      // compare the squre of the left and right element
      int left_sqaure = nums[left]*nums[left];
      int right_sqaure = nums[right]*nums[right];
      if(left_sqaure > right_sqaure) {
         // store the larger element to the new arr
         arr[k] = left_sqaure;
         left++;
      }
      else{
          arr[k] = right_sqaure;
          right--;
      }
      k--;
   }
   return arr;

}
```sh
