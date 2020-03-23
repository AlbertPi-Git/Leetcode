
# Generate Prime Numbers

```c++
void primeNumGenerate(std::vector<int> &tab, int maxVal){
    bool* validTab= new bool [maxVal+1];
    memset(validTab,1,sizeof(bool)*(maxVal+1));
    validTab[2]=1;
    int i=2;
    while(i<=maxVal){
        if(validTab[i]){
            tab.push_back(i);
            int j=2;
            while(i*j<=maxVal){
                validTab[i*j]=0;
                j++;
            }
        }
        i++;
    }
}
```