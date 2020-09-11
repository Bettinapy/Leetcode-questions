# TOP Interview 100

#### 1. Palindrome Number -easy

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

**Example 1:**

```
Input: 121
Output: true
```

**Example 2:**

```
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

```ruby
# @param {Integer} x
# @return {Boolean}
# if x < 0 => false
# if x != reversedX ? false : true
# def reverseNum
# reversedX = reversedX*10 + reversedX%10
def is_palindrome(x)
    return false if x < 0
    reversedX = reverseNum(x)
    if x == reversedX
        true
    else
        false
    end
end
    
def reverseNum(x)
    reversedX = 0 
    while x != 0
        reversedX = reversedX * 10 + x % 10 
        x = x/10 
    end
    reversedX
end
```

#### 2. Container With Most Water -medium

##### IJ index

Given *n* non-negative integers *a1*, *a2*, ..., *an* , where each represents a point at coordinate (*i*, *ai*). *n* vertical lines are drawn such that the two endpoints of line *i* is at (*i*, *ai*) and (*i*, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

**Note:** You may not slant the container and *n* is at least 2.

 

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

```ruby
# @param {Integer[]} height
# @return {Integer}
# height.length >=2
# area = (in - im) * min(an, am)
# area = 1 * 1 = 1
#      = 2 * 1 = 2
#      = 1 * 6 = 6
# 1. the widest case is when x1 = height[0] and x2 = height[height.length-1]
# 2. We start over from the widest case, check if height[x1] < height[x2]
#    if so, we need to move x1 to the next index because we may find a higher x1
#    if not, we need to move x2 to the previous index because we may find a higher x2
# 3. Compare and Return the max area until x1 == x2
def max_area(height)
    maxArea = 0
    x1 = 0
    # invoke length with ()
    x2 = height.length() -1   
    while x1 < x2
        maxArea = [maxArea, (x2-x1)*([height[x1],height[x2]].min)].max
        if height[x1] < height[x2]
            x1 += 1
        else
            x2 -= 1
        end
    end
    maxArea
end
```

#### 3. Integer to Roman

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

**Example 4:**

```
Input: 58
Output: "LVIII"
Explanation: L = 50, V = 5, III = 3.
```

**Example 5:**

```
Input: 1994
Output: "MCMXCIV"
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

```ruby
# @param {Integer} num
# @return {String}
# 1. while num != 0, then while num >= values, concatenate the correspoding str and substract the value from num, stop looping when num != values, add 1 to i

def int_to_roman(num)
    return "" if num < 1 || num > 3999
    
    values = [1000,900,500,400,100,90,50,40,10,9,5,4,1]
    strs = ["M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"]
    
    romanStr = ""
    i = 0 
    while num > 0 
        while num >= values[i] 
            num -= values[i] 
            romanStr += strs[i] 
        end
        i += 1 
    end
    romanStr
    
end
```

#### 4. Roman to Integer

```ruby
# @param {String} s
# @return {Integer}

def roman_to_int(s) #MCMXCIV
    values = [1,4,5,9,10,40,50,90,100,400,500,900,1000]
    symbols = ["I","IV","V","IX","X","XL","L","XC","C","CD","D","CM","M"]
    result = 0
    j = symbols.length - 1 
    i = 0
    while i < s.length 
        length = symbols[j].length 
        while s[i...length+i] == symbols[j] 
            result += values[j] 
            i = i + length
        end
        j -= 1 
    end
    result
end
```

#### 5. Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

```
Input: ["flower","flow","flight"]
Output: "fl"
```

```python
# 1. find the shortest string in the strs array
# 2. iterate through the shortest string, then iterate throught all the other strings in the string array, compare the character on the same index, if any different found, return the sliced string
# 3. finally return the shortest string
class Solution(object):
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        if not strs:
            return ""
        shortest = min(strs,key=len) 
        for i, ch in enumerate(shortest):
            for other in strs: 
                if other[i] != ch: 
                    
                    return shortest[:i]
        return shortest 
        
```

#### 6. 3 sum

Given an array `nums` of *n* integers, are there elements *a*, *b*, *c* in `nums` such that *a* + *b* + *c* = 0? Find all unique triplets in the array which gives the sum of zero.

Notice that the solution set must not contain duplicate triplets.

 

**Example 1:**

```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
```

```python
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        # sort nums
        nums.sort() #[-4,-1,-1,0,1,2]
        result = []
        # we need to find 3 numbers, so max i should be at the index of len(nums)-2
        for i in range(len(nums)-1): # (0,5)
            # while number is equal to its previous number, no need to find sum
            # avoid duplicates
            if i > 0 and nums[i] == nums[i-1]:
                continue
            key1 = nums[i] # -1
            sumKeys = -nums[i] # 1
            lo = i+1
            hi = len(nums) - 1 #5
            while lo < hi: # 0 + 1 = 1
                if nums[lo] + nums[hi] == sumKeys:
                    result.append([nums[i], nums[lo], nums[hi]])
                    while lo < hi and nums[lo] == nums[lo+1]:
                        lo += 1 
                    while lo < hi and nums[hi] == nums[hi-1]:
                        hi -= 1
                    lo += 1 
                    hi -= 1 
                elif nums[lo] + nums[hi] < sumKeys:
                    lo += 1 
                else:
                    hi -=1                 

        return result
                
            
        
```

#### 7. 3 Sum closest 

Given an array `nums` of *n* integers and an integer `target`, find three integers in `nums` such that the sum is closest to `target`. Return the sum of the three integers. You may assume that each input would have exactly one solution.

 

**Example 1:**

```
Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

```python
class Solution(object):
    def threeSumClosest(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        nums.sort() # [-1,-1,1,1,3]
        sums = nums[0] + nums[1] + nums[len(nums)-1] # 1
        for i in range(len(nums)-2): #(0,2)
            if i > 0 and nums[i] == nums[i-1]:
                continue
            key1 = nums[i] # -1
            lo = i + 1 # 1
            hi = len(nums)-1 # 4
            while lo < hi: # 1 < 2
                newSums = key1 + nums[lo] + nums[hi] # -1
                if target == newSums:
                        return newSums
                if abs(target-sums) > abs(target-newSums): # 2 > 0                   
                    sums = newSums # -1                                   

                if target < newSums:
                    hi -= 1
                if target > newSums:
                    lo += 1
        return sums
```

