### Longest Substring Without Repeating Characters
 
Given a string, find the length of the **longest substring** without repeating characters.

### Example

Input: `"abcabcbb"`

Output: 3 

Explanation: The answer is `"abc"`, with the length of 3. 




### Solution
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> map = new HashMap<>();
        int i = 0, j = 0, max = 0;
        for(int k = 0; k < s.length(); k++) {
            if(!map.containsKey(s.charAt(k))) {
                map.put(s.charAt(k), j++);
            }        
            else {
                if(map.get(s.charAt(k)) >= i) {
                    i = map.get(s.charAt(k)) + 1;
                    map.put(s.charAt(k), j++);
                    
                }
                else map.put(s.charAt(k), j++);
            }
            max = Math.max(max, j - i);
        }
        return max;
    }    
}
```

