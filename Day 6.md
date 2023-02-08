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
