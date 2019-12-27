# JianZhi_23 - Is Binary Search Tree

From post-order traversal result of a binary tree to verify whether this is a binary search tree.

## Initial idea
The last element is the root of this tree, use the root value to find the first element that is no less than the root in the sequence. Left subsequence is left tree, it should be empty or its max value is less than root. Then verify the right tree in the same way. 

```python
class Solution:
    def VerifySquenceOfBST(self, sequence):
        if not sequence:
            return False
        root=sequence[-1]
        i=0
        while sequence[i]<root:
            i+=1
        leftRes=(not sequence[:i]) or (max(sequence[:i])<root)
        rightRes=(not sequence[i:-1]) or (min(sequence[i:-1])>root)
        return leftRes and rightRes
```