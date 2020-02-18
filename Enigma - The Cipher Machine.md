# Enigma - The Cipher Machine

https://leetcode.com/discuss/interview-question/358108/Akuna-Capital-or-OA-2020-or-Software-Engineer-C%2B%2B

```c++
#include<vector>
#include<iostream>
#include<new>
#include<string.h>
#include<chrono>
class Solution {
    public:
        long long NumOfConfig(int rotorCnt, int minVal, int maxVal){
            long long totalConfigNum=0;
            //Only need to consider there are how many combinations between the 0th rotor and 1st rotor when 0th rotor is fixed, then a^(N-1) is the number of combinations for N rotors when 0th rotor is fixed. 
            for(unsigned int i=minVal;i<=maxVal;i++){
                int coPrimePairNum=0;
                for(unsigned int j=minVal;j<=maxVal;j++){
                    if(!(i|j)&1)    //If both are even number, then skip
                        continue;
                    if(1==gcd2(i,j))
                        coPrimePairNum++;
                }
                long long tmpConfigNum=powerN_mod(coPrimePairNum,rotorCnt-1,1000000007);
                totalConfigNum+=tmpConfigNum;
            }
            return totalConfigNum%1000000007;
        }

        //Three ways to implement greatest common divider function, gcd() and gcd3() are others' ideas, gcd2() is my intuitive version, surprisingly, it's the fastest one according to my test.
        unsigned int gcd(unsigned int a, unsigned int b){
            while(b){
                unsigned int t=a%b;
                a=b;
                b=t;
            }
            return a;
        }

        unsigned int gcd2(unsigned int a, unsigned int b){
            unsigned int t;
            while(t=std::min(a,b)){
                if(t==a){
                    b%=a;
                }else{
                    a%=b;
                }
            }
            return a?a:b;
        }

        unsigned int gcd3(unsigned int u, unsigned int v){
            auto shift = __builtin_ctz(u | v);
            u >>= __builtin_ctz(u);
            do {
                v >>= __builtin_ctz(v);
                if(u > v)
                    std::swap(u, v);
            } while((v -= u));
            return u << shift;
        }

        long long powerN_mod(long long base, int N, long long mod){
            if(N==1)
                return base%mod;
            long long res=(base*powerN_mod(base,N-1,mod))%mod;
            return res;
        }
};

int main(){
    Solution Sol=Solution();
    unsigned int startTime = std::chrono::duration_cast<std::chrono::milliseconds>(std::chrono::system_clock::now().time_since_epoch()).count();

    long long res=Sol.NumOfConfig(100,1,10000);

    unsigned int endTime = std::chrono::duration_cast<std::chrono::milliseconds>(std::chrono::system_clock::now().time_since_epoch()).count();
    std::cout<<res<<','<<endTime-startTime<<std::endl;
}
```
