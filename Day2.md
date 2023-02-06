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
   
   ```
   
   
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
```

## 209.长度最小的子数组
https://leetcode.com/problems/minimum-size-subarray-sum/
The key point to understand sliding window. where is the beginning and ending of the window, and when does the window's left change
- in the for loop, the right pointer move forward and calculate the sum of the elements
- check if the sum larger or equal to the target. calculate the length between two pointers,
- if it does, we will move the left pointer forward, and the sum will substrate the element of left pointer point to.


```sh

int min(int a, int b) {
    if(a<b){
        return a;
    }
    return b;
}
int minSubArrayLen(int target, int* nums, int numsSize){
    int left = 0;
    int right = 0;
    int result = INT_MAX;
    int sum =0;
    for(right = 0; right < numsSize ; right++) {
       sum += nums[right];
       while(sum >= target) {
           int min_length = right-left+1;
           result = min( min_length, result);
           sum = sum - nums[left];
           left ++;

       }
       
    }
    if(result == INT_MAX){
        return 0;
    }else{
        return result;
    }

}
```

 59.螺旋矩阵II


