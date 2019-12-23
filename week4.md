# 1. Algorithm
3. 无重复字符的最长子串<br>
给定一个字符串，请你找出其中不含有重复字符的最长子串的长度。<br>
``` java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        char[] chars = s.toCharArray();
        int maxLength = 0;
        int thisLoopLength = 0;
        Map<Character, Character> map = new HashMap();
        for (int i = 0; i < chars.length; i++) {
            thisLoopLength = 0;
            map.clear();
            for(int j = i; j < chars.length; j++) {
                if (map.containsKey(chars[j])) {
                    break;
                } else {
                    thisLoopLength ++;
                    map.put(chars[j], chars[j]);
                }
            }
            if (maxLength < thisLoopLength) {
                maxLength = thisLoopLength;
            }
        }
        return maxLength;
    }
}
```

# 2. review
