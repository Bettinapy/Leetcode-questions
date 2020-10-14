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

