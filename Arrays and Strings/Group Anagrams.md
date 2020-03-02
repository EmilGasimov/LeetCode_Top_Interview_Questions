### Group Anagrams

Given an array of strings, group anagrams together.

Example:

Input: `["eat", "tea", "tan", "ate", "nat", "bat"]`,

Output:

`[`
  `["ate","eat","tea"],`
  `["nat","tan"],`
  `["bat"]`
`]`

Note:

All inputs will be in lowercase.

The order of your output does not matter.

### Solution 1 [own]
```java
class Solution {
    private boolean areAnagrams(String a, String b) {
        if(a.length() != b.length()) return false;
        for(int i = 0; i < a.length(); i++) {
            if(!b.contains(a.subSequence(i, i+1))) return false;
            else b = b.replaceFirst(a.substring(i,i+1), "");
        }
        return b.equals("");
        
    }
    
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> anagrams = new ArrayList<>();
        if(strs.length == 0) return anagrams;
        List<String> list = new ArrayList<>();
        list.add(strs[0]);
        anagrams.add(list);
        //anagrams.add(Arrays.asList(strs[0]));
        String temp; boolean exists;
        for(int i = 1; i < strs.length; i++) {
            exists = false;
            for(int j = 0; j < anagrams.size(); j++) {   
                temp = strs[i];
                if(areAnagrams(anagrams.get(j).get(0), temp)) {
                    anagrams.get(j).add(strs[i]); 
                    exists = true;   
                    break; 
                }
            }
            if(exists == false) { 
                List<String> l = new ArrayList<>();
                l.add(strs[i]);
                anagrams.add(l);
                //anagrams.add(Arrays.asList(strs[i]));   -- this does not work; cannot add a new element to the list
            }
        }
        return anagrams;
    }
}
```

### Solution 2 [efficient]
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        if (strs == null || strs.length == 0) return new ArrayList<List<String>>();
        Map<String, List<String>> map = new HashMap<String, List<String>>();
        for (String s : strs) {
            char[] ca = s.toCharArray();
            Arrays.sort(ca);
            String keyStr = String.valueOf(ca);
            if (!map.containsKey(keyStr)) map.put(keyStr, new ArrayList<String>());
            map.get(keyStr).add(s);
        }
        return new ArrayList<List<String>>(map.values());
    }
}
```
### Solution 3 [without sorting - probably the best one]
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        
        Map<String, List<String>> map = new HashMap<>();
        for(String w : strs){
            String key = hash(w);          
            if(!map.containsKey(key)) map.put(key, new LinkedList<>());
            map.get(key).add(w);
        }
        
        return new ArrayList<>(map.values());
    }
    
    String hash(String s){
        int[] a = new int[26];
        for(char c : s.toCharArray()) a[c-'a']++;
        return Arrays.toString(a);
    }
}
```
