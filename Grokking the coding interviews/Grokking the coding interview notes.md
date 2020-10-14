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

#### 1.4 Smallest Subarray with a given sum

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

