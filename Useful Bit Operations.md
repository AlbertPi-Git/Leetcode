# Useful Bit Operations

## Get the max and min value of a integer type
```c++
int width=sizeof(typeA)*8;

//For signed type
//max=0111...1111
//min=1000...0000
typeA max=~(1<<width-1);
typeA min=1<<(width-1);

//For unsigned type
//max=1111...1111
//min=0000...0000
typeA max=~0;
typeA min=0;

```
