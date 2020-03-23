# Leetcode 468 - Validate IP Address

## Initial Idea
Simply validate whether each constraint is satisfied.

```python
class Solution:
    def validIPAddress(self, IP: str) -> str:
        IPv6CharsSet={'0','1','2','3','4','5','6','7','8','9','a','b','c','d','e','f'}
        IP=IP.lower()

        def IPv4Check(IP):
            groups=IP.split('.')
            if len(groups)!=4:
                return False
            for item in groups:
                try:
                    int(item)
                except:
                    return False
                if int(item)>255 or int(item)<0:
                    return False
                if int(item)!=0 and item[0]=='0':
                    return False
                if int(item)==0 and len(item)>1:
                    return False
            return True
        
        def IPv6Check(IP):
            groups=IP.split(':')
            if len(groups)!=8:
                return False
            for item in groups:
                if len(item)>4 or len(item)<1:
                    return False
                for char in item:
                    if char not in IPv6CharsSet:
                        return False
            return True
        
        if IPv4Check(IP):
            return "IPv4"
        if IPv6Check(IP):
            return "IPv6"
        return "Neither"
```