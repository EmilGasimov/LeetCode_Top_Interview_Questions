Given an unsorted array, return whether an increasing subsequence of length 3 exists or not.

### Solution [linear time, constant space]
(the point is, the order of `min` and `mid` does not matter; the function returns `true` if and only if there exists a number that is greater than `mid`.)

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
