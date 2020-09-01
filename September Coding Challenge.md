# September

#### Largest Time for Given Digits

Given an array of 4 digits, return the largest 24 hour time that can be made.

The smallest 24 hour time is 00:00, and the largest is 23:59. Starting from 00:00, a time is larger if more time has elapsed since midnight.

Return the answer as a string of length 5. If no valid time can be made, return an empty string.

```java
/* 1. Permutation: find all possible combinations and compare each of them one  by one to find the valid and largest time
	2. The sum of indexes is 0 + 1 + 2 + 3 = 6
	3. Time complexity is 4 * 4 * 4 = 64
*/


class Solution {
    public String largestTimeFromDigits(int[] A) {
        String time="";
        int l;
        for(int i=0; i<4; i++){
            for(int j=0; j<4; j++){
                for(int k=0; k<4; k++){
                    if( i==j || i==k || j==k) continue;
                    l = 6-i-j-k;
                    String h = "" + A[i] + A[j], m = "" + A[k] + A[l], t = h + ":" + m;
                    // use compareTo to compare to Strings lexicographically, the compare is based on the Unicode                        value 
                    if(h.compareTo("24")<0 && m.compareTo("59")<0 && time.compareTo(t)<0) time = t;
                }
            }
        }
        return time;
    }
}
```

