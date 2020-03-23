# Leetcode 49 - GroupAnagrams 

## My initial idea: 
if two words are anagrams, times each letter appears in both words must be the same, so just use a frequency vector as the key of hashmap to classify words to different group.

```python
from collections import defaultdict
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        dic=defaultdict(list)
        for word in strs:
            counter=[0]*26
            for letter in word:
                counter[ord(letter)-ord('a')]+=1
            key=''
            for cnt in counter:
                key+=str(cnt)
            dic[key].append(word)
        return dic.values()
```

## Others' idea 1
The crucial point of this problem is to choose a proper key of hashmap. If two words are anagrams, besides frequency vector, their sorted results are also the same, so that can also be used as the key of hashmap.

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        res = []
        dic = {}
        for s in strs:
            keys = "".join(sorted(s))
            if keys not in dic:
                dic[keys] = [s]
            else:
                dic[keys].append(s)
        return list(dic.values())
```