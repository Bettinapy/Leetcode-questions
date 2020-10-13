# TOP Bloomberg Interview Questions

#### 1. Valid Anagram (easy)

Given two strings *s* and *t* , write a function to determine if *t* is an anagram of *s*.

**Example 1:**

```
Input: s = "anagram", t = "nagaram"
Output: true
```

**Example 2:**

```
Input: s = "rat", t = "car"
Output: false
```

```python
#1. iterate thru s, generate a hash, key is the character and value is the number of times the character appears in s
#2. iterate thru t, if the char exists in the hash, substract 1 from its corresponding value. if the char not exists in the 
#3. check the values in the hash
"""
chars = {}
for char in s:
    # generate key value pairs
for char2 in t:
    if char[char2]:
        # substract the value in chars hash
    else:
        # generate a new key value pair
if all(values==0 for value in chars.values())
"""

class Solution(object):
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        chars = {}
        for char in s:
            if char in chars:
                chars[char] += 1
            else:
                chars[char] = 1 # chars = {"r":1, "a":1, "t":1}

        for char2 in t:
            if char2 in chars:
                chars[char2] -= 1
            else:
                chars[char2] = 1

        return all(values == 0 for values in chars.values())
# time complexity: O(n), space complexity: O(1)
```

