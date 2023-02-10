##242.有效的字母异位词
https://leetcode.com/problems/valid-anagram/
- this problem is to find out if two words has same characters. 
- we know that there are 26 letters, and can represent in number
- create a list count[] and iterate the first word, each time we record the character to coresponding num 
- ex; aram  we find a, then count[ord(c) - ord('a')] +=1
- then iterate the second word, for each character, we -1
- if there's one element is not zero, then they are not the same.
```sh
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        counts = [0] * 26
        for c in s:
            counts[ord(c) - ord("a")] += 1
        for j in t: 
            counts[ord(j) - ord("a")] -= 1
        for i in range(26):
            if counts[i] != 0 :
                return False
        return True
        
 ```
 
  use dictionary
  ```sh
  class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s)!= len(t):
            return False
        dic = {}
        for char in s:
            if char in dic:
                dic[char] += 1
            else:
                dic[char] = 1
        for char in t:
            if char in dic:
                dic[char] -= 1
        for char in dic:
            if dic[char] != 0:
                return False
        return True
 
 ```
 
 use counter
 ```sh
 class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        counter = {}
        counter2 = {}
        for char in s:
            counter[char] = counter.get(char,0)+1
        for char in t:
            counter2[char] = counter2.get(char,0) +1
        return counter == counter2
            
```

##349. 两个数组的交集


 ```sh
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        res = {}
        ans = []
        for num in nums1:
            res[num] = 1
        for n in nums2:
            if n in res.keys() and res[n] == 1 :
                ans.append(n)
                res[n] = 0

        return ans

 ```
 
 using Counter and set
 set is to avoid adding duplicate numbers
 ```sh
 class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]: 
        from collections import Counter
        c = Counter(nums1)
        output = set()
        for n in nums2:
            if n in c:
                output.add(n)

        return output
 
```
## 1. two sum
https://leetcode.com/problems/two-sum/solutions/

```sh
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        
      numDict = {}
      for i, num in enumerate(nums):
          diff = target-num
          if diff in numDict:
              return [ numDict[diff], i]
          else:
              numDict[num]=i
      return
 
```

 ##202. Happy Number          
        
https://leetcode.com/problems/happy-number/
```sh
class Solution:
    def isHappy(self, n: int) -> bool:
        nums = set()
        # n == 1 or find n in the set 
        while n:
            n = self.sumOfSquare(n)
            if n == 1:
                return True
            if n in nums:
                return False
            else:
                nums.add(n)
                
 

    def sumOfSquare(self, n: int) -> int:
        # 19 first 19 mod 10  =9
         # second 19 // 10 = 1
        sum = 0
        while n != 0:
            sum += (n % 10) ** 2
            n  = n // 10
        return sum
     ```
