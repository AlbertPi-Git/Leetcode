# JianZhi 46 - Johseph Ring

## Initial Idea
Simulation with linked list, but TLE.

```c++
struct MyNode{
    int num;
    MyNode* prev;
    MyNode* next;
    MyNode(int x): num(x),prev(nullptr),next(nullptr){}
};

class Solution {
public:
    int lastRemaining(int n, int m) {
        MyNode* head=new MyNode(0);
        MyNode* prev=head;
        for(int i=1;i<n;i++){
            MyNode* tmp=new MyNode(i);
            prev->next=tmp;
            tmp->prev=prev;
            prev=tmp;
        }
        prev->next=head;
        head->prev=prev;

        int cnt=n;
        while(cnt>1){
            for(int i=1;i<m;i++){
                head=head->next;
            }
            cnt--;
            MyNode* toDel=head;
            head=head->next;
            toDel->prev->next=toDel->next;
            toDel->next->prev=toDel->prev;
            delete toDel;
        }
        return head->num;      
    }
};
```

## Others' Idea 1
DP
```c++
class Solution {
public:
    int lastRemaining(int n, int m) {
        std::vector<int> dp(n,0);
        for(int i=1;i<n;i++){
            dp[i]=(dp[i-1]+m)%(i+1);
        }
        return dp[n-1];
    }
};
```

```c++
class Solution {
public:
    int lastRemaining(int n, int m) {
        int res=0;
        for(int i=1;i<n;i++){
            res=(res+m)%(i+1);
        }
        return res;
    }
};
```