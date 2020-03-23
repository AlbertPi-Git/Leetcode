# JianZhi 44 - Reverse Sentence

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        tmp=s.strip().split(" ")
        words=[]
        for word in tmp:
            if word!="":
                words.append(word)
        print(words)
        front=words[:len(words)//2]
        back=words[len(words)//2:]
        return " ".join(back[-1::-1]+front[-1::-1])
```