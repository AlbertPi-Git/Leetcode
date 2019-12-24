# JianZhi_4 - Implement Queue with Stacks

## Initial idea
Use one stack to contain all elements, use the other stack to reverse the order and do pop/peek
```python
class MyQueue:

    def __init__(self):
        self.stack1=[]
        self.stack2=[]
        

    def push(self, x: int) -> None:
        self.stack1.append(x)
        

    def pop(self) -> int:
        while self.stack1:
            self.stack2.append(self.stack1.pop())
        top=self.stack2.pop()
        while self.stack2:
            self.stack1.append(self.stack2.pop())
        return top

        
    def peek(self) -> int:
        while self.stack1:
            self.stack2.append(self.stack1.pop())
        top=self.stack2[-1]
        while self.stack2:
            self.stack1.append(self.stack2.pop())
        return top
        

    def empty(self) -> bool:
        return len(self.stack1)==0
```