# JianZhi_19 LC_155 - Min Stack

## Others' idea 1
Use another stack to record all historical min values that are still in stack. So when push, compare with top element of the minStack (Note that if it's equal to current min, also need to push into minStack, or may cause getMin from an empty minStack). When pop, if it's current min value, then also pop it from the minStack.

```python
class MinStack:

    def __init__(self):
        self.stack=[]
        self.minStack=[2**32-1]
        
    def push(self, x: int) -> None:
        self.stack.append(x)
        if x<=self.minStack[-1]:
            self.minStack.append(x)
        

    def pop(self) -> None:
        top=self.stack.pop()
        if top==self.minStack[-1]:
            self.minStack.pop()
        return top

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.minStack[-1]
```