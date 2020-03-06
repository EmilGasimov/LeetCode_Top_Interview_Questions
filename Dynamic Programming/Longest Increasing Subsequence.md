Given an unsorted array of integers, find the length of longest increasing subsequence.

Example:

`Input: [10,9,2,5,3,7,101,18]`

`Output: 4 `

`Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. `


### Solution [own]
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if(nums == null || nums.length == 0) return 0;
        if(nums.length == 1) return 1;
        int n = nums.length;
        int[] array = new int[n]; 
        int max = array[0];
        Arrays.fill(array, 1);
        for(int i = 1; i < n; i++) {
            for(int j = 0; j < i; j++) {
                if(nums[i] > nums[j] && array[j] >= array[i]) {
                    array[i] = 1 + array[j];
                }
            }
            max = Math.max(array[i], max);
        }
        return max;
    }
}
```
