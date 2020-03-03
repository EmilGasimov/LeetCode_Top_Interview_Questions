Given an unsorted array, return whether an increasing subsequence of length 3 exists or not.

### Solution [linear time, constant space]

```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        int min = Integer.MAX_VALUE, mid = Integer.MAX_VALUE;
        for (int n : nums) {
            if (n < min) min = n;
            else if (n != min && n < mid) mid = n;            
            else if (n > mid) return true;
        }
        
        return false;
    }
 }
 ```
