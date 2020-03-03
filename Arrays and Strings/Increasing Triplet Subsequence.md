Given an unsorted array, return whether an increasing subsequence of length 3 exists or not.

### Solution [linear time, constant space]

`min` - the min value.

`secondMin` - the smallest second value: the smallest value that has something before it that is even smaller. That 'something before it that is even smaller' does not have to be the current min value.


```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        int min = Integer.MAX_VALUE, secondMin = Integer.MAX_VALUE;
        for (int n : nums) {
            if (n < min) min = n;
            else if (n != min && n < secondMin) mid = n;            
            else if (n > secondMin) return true;
        }
        
        return false;
    }
 }
 ```
