### Increasing Triplet Subsequence
Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.

Formally the function should return true if there exists i, j, k
such that arr[i] < arr[j] < arr[k] given 0 ≤ i < j < k ≤ n-1 and return false otherwise.




### Solution
The main idea is to keep track of the two values when checking all the elements in the array: the minimum value min until now and the second minimum value secondMin from the minimum value's position until now. Then if we can find the third one that larger than those two values at the same time, it must exists the triplet subsequence and return true.

What need to be careful is: we need to include the condition that some value has the same value with minimum number, otherwise this condition will cause the secondMin change its value.
```java
public boolean increasingTriplet(int[] nums) {
    // start with two largest values, as soon as we find a number bigger than both, while both have been updated, return true.
    int small = Integer.MAX_VALUE, big = Integer.MAX_VALUE;
    for (int n : nums) {
        if (n <= small) { small = n; } // update small if n is smaller than both
        else if (n <= big) { big = n; } // update big only if greater than small but smaller than big
        else return true; // return if you find a number bigger than both
    }
    return false;
}
```
