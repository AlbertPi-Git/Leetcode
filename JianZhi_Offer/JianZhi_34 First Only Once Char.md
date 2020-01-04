# JianZhi_34 - First Only Once Char

## Initial idea
Use hash map record counter of each char.
```python
from collections import defaultdict
class Solution:
    def FirstNotRepeatingChar(self, s):
        dic=defaultdict(int)
        for char in s:
            dic[char]+=1
        for i in range(len(s)):
            if dic[s[i]]==1:
                return i
        return -1
```
