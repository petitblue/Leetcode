## 977.有序数组的平方 
https://leetcode.com/problems/squares-of-a-sorted-array/description/

- this is an easy problem, it allows you to create an new array and restore the squred results in ascending order
- in the new arr, the return size is the same as the given array's
An intuition way of solving this problem is to store new value in the array, and sort it
```sh
int cmpfunc (const void * a, const void * b) {
   return ( *(int*)a - *(int*)b );
}int* sortedSquares(int* nums, int numsSize, int* returnSize){

   *returnSize =numsSize;
   for(int i = 0; i<numsSize; i++) {
       nums[i]=nums[i]*nums[i];
   }
   qsort(nums, numsSize, sizeof(int), cmpfunc );
   return nums;
   }
   
   ```sh
- the given array is an non decending order, that means that the largest squared value of the elements will appear on the front or back of the given array. So we can use a left and right pointer to make this possible.
- when we iterate the array from the left handside, we will store the larger value to the back of the new array(
-  (we know that the largest squared value will be only chosen from the first or last position.)
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


