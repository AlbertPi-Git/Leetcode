# Find Prime Factor

```c++
void prim(int m, int n)
 {
     if (m >= n)
     {
        while(m%n) n++;
        m/=n;
        prim(m, n);
        std::cout << n << std::endl;
     }
 }
```