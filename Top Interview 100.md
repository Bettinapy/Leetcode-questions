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

