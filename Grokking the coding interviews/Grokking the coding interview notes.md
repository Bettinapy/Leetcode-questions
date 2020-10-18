# Grokking the coding interview

### 1. Sliding window

#### 1.1 Introduction

Q: Given an array, find the average of all contiguous subarrays of size ‘K’ in it.

```
Array: [1, 3, 2, 6, -1, 4, 1, 8, 2], K=5
```

1. brutal force: calculate the sum of every 5-element continuous subarray (O(n)) of given array and divide the sum by 5 to find the average (O(k)). O(n*k) time complexity
2. sliding window: 
   1. where can be improved? For two consecutive subarrays of size "5", the overlapping part will be evaluated twice.
   2. Solution: 1. visualize each continuous subarray as a sliding window of 5 elements. When we move on to the next subarray, we will slide the window by one element. 2. Reuse the sum from the previous subarray, we can substract the element going out of the window and add the element now being included in the sliding window. 
   3. This will save us from going through the whole subarray to find the sum and as a result, the algorithm complexity will reduce to O(N)

#### 1.2 Maximum Sum Subarray of Size K

```python
def max_sub_array_of_size_k(k, arr):
  # TODO: Write your code here
  '''
  1. brutal force
  # 1. iterate thru subarrays
  # 2. calculate the sum, compare it with the previous sum
  # 2 + 1 + 5 = 8
  # largest_sum = arr[0] # 2
  # for i in range(len(arr)-k+1): #(0,3)
  #   subSum = arr[i] # 2
  #   for j in range(1, k):
  #     subSum += arr[i+j] # 5
  #   if subSum > largest_sum:
  #     largest_sum = subSum #7 
  # return largest_sum
  '''

  '''
  2. Sliding window
  '''
  subSum = 0
  maxSum = 0
  for i in range(k):
    subSum += arr[i]

  for startWin in range(1, len(arr)-k+1):
    subSum -= arr[startWin-1]
    subSum += arr[startWin+k-1]
    maxSum = max(subSum, maxSum)
  return maxSum

```

#### 1.3 Smallest Subarray with a given sum

Given an array of positive numbers and a positive number ‘S’, find the length of the **smallest contiguous subarray whose sum is greater than or equal to ‘S’**. Return 0, if no such subarray exists.

**Example 1:**

```
Input: [2, 1, 5, 2, 3, 2], S=7 
Output: 2
Explanation: The smallest subarray with a sum great than or equal to '7' is [5, 2].
```

```python
import math
def smallest_subarray_with_given_sum(s, arr):
  # TODO: Write your code here
  # 1. add-up elements until the sum becomes >= s, remember the length of this window as the smallest window so far
  # 2. slide the window in a stepwise fashion
  # 3. In each step, try to shrink the window until the sum < s and do two things: 
  #   1. if the current window is the smallest, replace it 
  #   2. substart the first element of the window to shrink the window
  
  arr_Sum = 0
  smallest_win = math.inf
  winStart = 0
  for winEnd in range(len(arr)):
    arr_Sum += arr[winEnd]
    while arr_Sum >= s:
      smallest_win = min(smallest_win, winEnd-winStart+1)
      arr_Sum -= arr[winStart]
      winStart += 1
  if smallest_win == math.inf:
    return 0
  return smallest_win

```

#### 1.4 Longest Substring with K Distinct Characters

Given a string, find the length of the **longest substring** in it **with no more than K distinct characters**.

**Example 1:**

```
Input: String="araaci", K=2
Output: 4
Explanation: The longest substring with no more than '2' distinct characters is "araa".
```

```python
def longest_substring_with_k_distinct(str, k):
  # TODO: Write your code here
  # 1. insert characters from the beginning of the string, until we have K distinct characters in the HashMap
  # 2. keep adding characters in a stepwise fashion
  # 3. try to shrink the string from the beginning if the count of characters is > K, while shrinking, decrement the count of chars in HashMap
  # 4. check if the current window is the longest so far
  longest_len = 0
  subStart = 0
  substr = {}
  
  for subEnd in range(len(str)):
    right_char = str[subEnd]
    if right_char not in substr:
      substr[right_char] = 0
    substr[right_char] += 1

    # shrink the string from the beginning of the window while the count of chars in substr is > k
    while len(substr) > k:
      left_char = str[subStart]
      substr[left_char] -= 1
      if substr[left_char] == 0:
        del substr[left_char]
      subStart += 1
    
    # check if the current window is the longest so far
    longest_len = max(longest_len, subEnd-subStart+1)
  
  return longest_len
     
```

#### 1.5 Fruits into Baskets

Given an array of characters where each character represents a fruit tree, you are given **two baskets** and your goal is to put **maximum number of fruits in each basket**. The only restriction is that **each basket can have only one type of fruit**.

You can start with any tree, but once you have started you can’t skip a tree. You will pick one fruit from each tree until you cannot, i.e., you will stop when you have to pick from a third fruit type.

Write a function to return the maximum number of fruits in both the baskets.

**Example 1:**

```
Input: Fruit=['A', 'B', 'C', 'A', 'C']
Output: 3
Explanation: We can put 2 'C' in one basket and one 'A' in the other from the subarray ['C', 'A', 'C']
```

```python
def fruits_into_baskets(fruits):
  window_start = 0
  max_length = 0
  fruit_frequency = {}

  # try to extend the range [window_start, window_end]
  for window_end in range(len(fruits)):
    right_fruit = fruits[window_end]
    if right_fruit not in fruit_frequency:
      fruit_frequency[right_fruit] = 0
    fruit_frequency[right_fruit] += 1

    # shrink the sliding window, until we are left with '2' fruits in the fruit frequency dictionary
    while len(fruit_frequency) > 2:
      left_fruit = fruits[window_start]
      fruit_frequency[left_fruit] -= 1
      if fruit_frequency[left_fruit] == 0:
        del fruit_frequency[left_fruit]
      window_start += 1  # shrink the window
    max_length = max(max_length, window_end-window_start + 1)
  return max_length


```

#### 1.6 *No-repeat Substring (hard!!)

Given a string, find the **length of the longest substring** which has **no repeating characters**.

**Example 1:**

```
Input: String="aabccbb"
Output: 3
Explanation: The longest substring without any repeating characters is "abc".
```

```python
# we don't need to delete the non-existing key value pair in the sliding window, we can just keep them

def non_repeat_substring(str1):
  window_start = 0
  max_length = 0
  char_index_map = {}

  # try to extend the range [windowStart, windowEnd]
  for window_end in range(len(str1)):
    right_char = str1[window_end]
    # if the map already contains the 'right_char', shrink the window from the beginning so that
    # we have only one occurrence of 'right_char'
    if right_char in char_index_map:
      # this is tricky; 
      # in the current window, we will not have any 'right_char' after its previous index
      # and if 'window_start' is already ahead of the last index of 'right_char', we'll keep 'window_start'
      window_start = max(window_start, char_index_map[right_char] + 1)
    # insert the 'right_char' into the map
    char_index_map[right_char] = window_end
    # remember the maximum length so far
    max_length = max(max_length, window_end - window_start + 1)
  return max_length
```

#### 1.7 *Longest substring with same letter after replacement (hard!!)

Given a string with lowercase letters only, if you are allowed to **replace no more than ‘k’ letters** with any letter, find the **length of the longest substring having the same letters** after replacement.

**Example 1:**

```
Input: String="aabccbb", k=2
Output: 5
Explanation: Replace the two 'c' with 'b' to have a longest repeating substring "bbbbb".
```

```python

# 1. Iterate throught the string to add one letter at a time in the window
# 2. Keep track of the count of the maximum repeating letter (max_repeating_letter) in the window, get the number of repeating
#    letters by substracting max_repeating_letter from the len(sliding_window)
# 3. shrink the window if the number of ramining letters is > k

def length_of_longest_substring(str, k):
  # TODO: Write your code here
  window_start, max_repeating_letter, longest_substr = 0, 0, 0
  strs_collection = {}

  for window_end in range(len(str)):
    right_char = str[window_end]
    if right_char not in strs_collection:
      strs_collection[right_char] = 0
    strs_collection[right_char] += 1
    # this is trick. keep track of the maximum repeating letter, can be the current char, or the previous one
    max_repeating_letter = max(max_repeating_letter, strs_collection[right_char])

    # shrink the window when the number of remaining letters is > k
    if (window_end - window_start + 1 - max_repeating_letter) > k:
      left_char = str[window_start]
      strs_collection[left_char] -= 1
      window_start += 1
    
    longest_substr = max(longest_substr, window_end - window_start + 1)

  return longest_substr

```

#### 1.8 Longest subarray with ones after replacement (hard!) similar to 1.7

Given an array containing 0s and 1s, if you are allowed to **replace no more than ‘k’ 0s with 1s**, find the length of the **longest contiguous subarray having all 1s**.

**Example 1:**

```
Input: Array=[0, 1, 1, 0, 0, 0, 1, 1, 0, 1, 1], k=2
Output: 6
Explanation: Replace the '0' at index 5 and 8 to have the longest contiguous subarray of 1s having length 6.
```

```python
# 1. iterate through the array, keep track of the frequency of 1 (occur_1) in the sliding window
# 2. get the remaining number of letters by substracting occur_1 from the len(sliding_window)
# 3. if the remaining number is > k, then shrink my sliding window:
#   1. decrement the frequency of 1
#   2. take out the first element in the sliding window
# 4. check if the current sliding window is the longest one

def length_of_longest_substring(arr, k):
  # TODO: Write your code here
  frequency_1, window_start, longest_substr = 0, 0, 0

  for window_end in range(len(arr)):
    right_num = arr[window_end]
    if right_num == 1:
      frequency_1 += 1
    
    if (window_end - window_start + 1 - frequency_1) > k:
      left_num = arr[window_start]
      if left_num == 1:
        frequency_1 -= 1
      window_start += 1
    
    longest_substr = max(longest_substr, window_end - window_start + 1)

  return longest_substr

```

#### 1.9 * Problem Challenge 1 (hard!!)

Given a string and a pattern, find out if the **string contains any permutation of the pattern**.

```python
def find_permutation(str1, pattern): #oidbcaf, abc
  window_start, matched = 0, 0
  char_frequency = {}

  for chr in pattern:
    if chr not in char_frequency:
      char_frequency[chr] = 0
    char_frequency[chr] += 1 #{a:1, b:1, c:1}

  # our goal is to match all the characters from the 'char_frequency' with the current window
  # try to extend the range [window_start, window_end]
  for window_end in range(len(str1)): #(0,7)
    right_char = str1[window_end] # b
    if right_char in char_frequency:
      # decrement the frequency of matched character
      char_frequency[right_char] -= 1
      if char_frequency[right_char] == 0:
        matched += 1 # 1 {a:1, b:0, c:1}

    if matched == len(char_frequency):
      return True

    # this is tricky. shrink the window by one character as long as window_end is >= the length of pattern.
    if window_end >= len(pattern) - 1:
      left_char = str1[window_start]
      window_start += 1
      if left_char in char_frequency:
        if char_frequency[left_char] == 0:
          matched -= 1
        char_frequency[left_char] += 1

  return False


def main():
  print('Permutation exist: ' + str(find_permutation("oidbcaf", "abc")))
  print('Permutation exist: ' + str(find_permutation("odicf", "dc")))
  print('Permutation exist: ' + str(find_permutation("bcdxabcdy", "bcdyabcdx")))
  print('Permutation exist: ' + str(find_permutation("aaacb", "abc")))


main()

```



### 2. Two Pointers

Given an array of sorted numbers and a target sum, find a **pair in the array whose sum is equal to the given target**.

Write a function to return the indices of the two numbers (i.e. the pair) such that they add up to the given target.

**Example 1:**

```
Input: [1, 2, 3, 4, 6], target=6
Output: [1, 3]
Explanation: The numbers at index 1 and 3 add up to 6: 2+4=6
```

#### 2.1 Pair with Target Sum

```python
# 1. two pointer. one at the beginning, another at the end
# 2. calculat the sum of two pointers, compare the sum with the target
#   1. if sum < target_sum, increment the start pointer
#   2. if sum > target_sum, decrement the end pointer
#   3. if ==, return [start_pointer, end_pointer]
# 3. compare while start < end

def pair_with_targetsum(arr, target_sum):
  # TODO: Write your code here
  start_pointer, end_pointer = 0, len(arr) - 1
  while start_pointer < end_pointer:
    pair_sum = arr[start_pointer] + arr[end_pointer]
    if pair_sum < target_sum:
      start_pointer += 1
    elif pair_sum > target_sum:
      end_pointer -= 1
    else:
      return [start_pointer, end_pointer]

  return [-1,-1]

```

HashTable:

```python
def pair_with_targetsum(arr, target_sum):
  nums = {}  # to store numbers and their indices
  for i, num in enumerate(arr):
    if target_sum - num in nums:
      return [nums[target_sum - num], i]
    else:
      nums[arr[i]] = i
  return [-1, -1]


def main():
  print(pair_with_targetsum([1, 2, 3, 4, 6], 6))
  print(pair_with_targetsum([2, 5, 9, 11], 11))


main()

```

#### 2.2 *Remove Duplicates (easy) but hard to think

Given an array of sorted numbers, **remove all duplicates** from it. You should **not use any extra space**; after removing the duplicates in-place return the length of the subarray that has no duplicate in it.

**Example 1:**

```
Input: [2, 3, 3, 3, 6, 9, 9]
Output: 4
Explanation: The first four elements after removing the duplicates will be [2, 3, 6, 9].
```

```python
# 1. Shift the element whenever we encounter duplicates. 
# 2. One pointer to iterate the ele in the arr, one pointer for replacing the Next non-duplicate number

def remove_duplicates(arr): #[2,3,3,3,6,9,9]
  # index of the next non-duplicate element
  next_non_duplicate = 1

  i = 1
  while(i < len(arr)):
    if arr[next_non_duplicate - 1] != arr[i]: 
      arr[next_non_duplicate] = arr[i] 
      next_non_duplicate += 1 
    i += 1 

  return next_non_duplicate

```

**Problem 2:** Given an unsorted array of numbers and a target ‘key’, remove all instances of ‘key’ in-place and return the new length of the array.

**Example 2:**

```
Input: [3, 2, 3, 6, 3, 10, 9, 3], Key=3
Output: 4
Explanation: The first four elements after removing every 'Key' will be [2, 6, 10, 9].
```

```python
def remove_element(arr, key):
  nextElement = 0  # index of the next element which is not 'key'
  for i in range(len(arr)):
    if arr[i] != key:
      arr[nextElement] = arr[i]
      nextElement += 1

  return nextElement


```

#### 1.3 Squaring a sorted array 

Given a sorted array, create a new array containing **squares of all the number of the input array** in the sorted order.

**Example 1:**

```
Input: [-2, -1, 0, 2, 3]
Output: [0, 1, 4, 4, 9]
```

```python
# 1. two pointers, one at the end left, one at the end right, compare their squares
# 2. if left square < right square, add right square to the array, move right pointer to the previous number; else, opposite

def make_squares(arr):
  # TODO: Write your code here
  arr_len = len(arr)
  squares = [0 for i in range(arr_len)]
  left_pointer, right_pointer = 0, arr_len - 1

  highestSquareIdx = arr_len - 1

  while left_pointer <= right_pointer: # '=' here to make sure that we compare ALL the numbers
    left_square = arr[left_pointer] * arr[left_pointer]
    right_square = arr[right_pointer] * arr[right_pointer]
    if left_square < right_square:
      squares[highestSquareIdx] = right_square
      right_pointer -= 1
    else:
      squares[highestSquareIdx] = left_square
      left_pointer += 1
    highestSquareIdx -= 1

  return squares

```

#### 1.4 Triple sum to zero (3 sum)

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
        # we need to find 3 numbers, so max i should be at the index of len(nums)-3
        for i in range(len(nums)-2): # (0,5)
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

#### 1.5 *Triplet Sum Close to Target (medium)

```python
import math


def triplet_sum_close_to_target(arr, target_sum):
  arr.sort()
  smallest_difference = math.inf
  for i in range(len(arr)-2):
    left = i + 1
    right = len(arr) - 1
    while (left < right):
      target_diff = target_sum - arr[i] - arr[left] - arr[right]
      if target_diff == 0:  # we've found a triplet with an exact sum
        return target_sum - target_diff  # return sum of all the numbers

      # the second part of the following 'if' is to handle the smallest sum when we have more than one solution
      if abs(target_diff) < abs(smallest_difference)or (abs(target_diff) == abs(smallest_difference) and target_diff > smallest_difference):
        smallest_difference = target_diff  # save the closest and the biggest difference

      if target_diff > 0:
        left += 1  # we need a triplet with a bigger sum
      else:
        right -= 1  # we need a triplet with a smaller sum

  return target_sum - smallest_difference
```

Time: O(N*logN + N^2)

Space: O(N)  (sort)

#### 1.6 Triplets with smaller sum

Given an array `arr` of unsorted numbers and a target sum, **count all triplets** in it such that **`arr[i] + arr[j] + arr[k] < target`** where `i`, `j`, and `k` are three different indices. Write a function to return the count of such triplets.

**Example 1:**

```
Input: [-1, 0, 2, 3], target=3 
Output: 2
Explanation: There are two triplets whose sum is less than the target: [-1, 0, 3], [-1, 0, 2]
```

```python
# iterate through the arr, first number. skip duplicated number
# two pointers, second and third number.  compare the sum of the three numbers with target. skip duplicated number

def triplet_with_smaller_sum(arr, target):
  arr.sort() # [-1,0,2,3], 3
  count = 0
  # TODO: Write your code 
  for i in range(len(arr) - 2): #(0,1)
    if i > 0 and arr[i - 1] == arr[i]:
      continue
    left = i + 1 # 1
    right = len(arr) - 1 # 3

    while left < right: # 1 < 3
      three_sum = arr[i] + arr[left] + arr[right] # 
      if three_sum < target:
        while left < right and arr[right] == arr[right - 1]:
          right -= 1
        while left < right and arr[left] == arr[left + 1]:
          left += 1
        # since arr[right] >= arr[left], therefore, we can replace arr[right] by any number between
        # left and right to get a sum less than the target sum
        count += right - left
        left += 1
      else:
        right -= 1
  return count
```

Time complexity: (O(N*logN + N^2))

Space: O(N)

Similar problem:

**Problem:** Write a function to return the list of all such triplets instead of the count. How will the time complexity change in this case?

```python
def triplet_with_smaller_sum(arr, target):
  arr.sort()
  triplets = []
  for i in range(len(arr)-2):
    search_pair(arr, target - arr[i], i, triplets)
  return triplets


def search_pair(arr, target_sum, first, triplets):
  left = first + 1
  right = len(arr) - 1
  while (left < right):
    if arr[left] + arr[right] < target_sum:  # found the triplet
      # since arr[right] >= arr[left], therefore, we can replace arr[right] by any number between
      # left and right to get a sum less than the target sum
      for i in range(right, left, -1):
        triplets.append([arr[first], arr[left], arr[i]])
      left += 1
    else:
      right -= 1  # we need a pair with a smaller sum
```

Time: O(N*logN + N^3)

Space: O(N)



#### 1.7 Subarrays with Product Less than a Target (time complexity?)

Given an array with positive numbers and a target number, find all of its contiguous subarrays whose **product is less than the target number**.

**Example 1:**

```
Input: [2, 5, 3, 10], target=30 
Output: [2], [5], [2, 5], [3], [5, 3], [10]
Explanation: There are six contiguous subarrays whose product is less than the target.
```

hint: using sliding window and two pointers

```python
from collections import deque


def find_subarrays(arr, target):
  result = []
  product = 1
  left = 0
  for right in range(len(arr)):
    product *= arr[right]
    while (product >= target and left < len(arr)):
      product /= arr[left]
      left += 1
    # since the product of all numbers from left to right is less than the target therefore,
    # all subarrays from left to right will have a product less than the target too; to avoid
    # duplicates, we will start with a subarray containing only arr[right] and then extend it
    # this is tricky: we use deque() to append element from right to left to avoid duplicates
    temp_list = deque()
    # we want to include left, so end should be left - 1
    for i in range(right, left-1, -1):
      temp_list.appendleft(arr[i])
      # append the list because append will mutate the subarray
      result.append(list(temp_list))
  return result
```

Time: O(N^3)

Space: O(N + N^2) N for temp list and N^2 for output list

