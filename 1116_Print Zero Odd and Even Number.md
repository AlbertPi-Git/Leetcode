# Leetcode 1116 - Print Zero Odd and Even Number

## Initial Idea
No deadlock, but TLE on LC in 51 case. Suppose it's total time TLE, after all this method is not synchronizing methods, it's just three methods races for the lock.
```c++
class ZeroEvenOdd {
private:
    int n;
    int state;  //0 means should print 0, then switch to state 1
                //1 means should print odd number, then switch to state 2
                //2 means should print 0, then switch to state 3
                //3 means should print even number, then switch to 0
    int curOdd;
    int curEven;
    std::mutex mtx;

public:
    ZeroEvenOdd(int n) {
        this->n = n;
        this->state=0;
        this->curOdd=1;
        this->curEven=2;
    }

    void printNumber(int x){
        std::cerr<<x;
    }

    // printNumber(x) outputs "x", where x is an integer.
    void zero() {
        while(true){
            mtx.lock();
            if(curOdd>n+1||curEven>n+1){
                mtx.unlock();
                break;
            }
            if(state==0||state==2){
                printNumber(0);
                state=(state+1)%4;
            }
            mtx.unlock();
        }
    }

    void odd() {
        while(true){
            mtx.lock();
            if(curOdd>n){
                mtx.unlock();
                break;
            }
            if(state==1){
                printNumber(curOdd);
                state=(state+1)%4;
                curOdd+=2;
            }
            mtx.unlock();
        }
    }

    void even() {
        while(true){
            mtx.lock();
            if(curEven>n){
                mtx.unlock();
                break;
            }
            if(state==3){
                printNumber(curEven);
                state=(state+1)%4;
                curEven+=2;
            }
            mtx.unlock();
        }
    }
};

int main(){
    ZeroEvenOdd obj(9);
    std::thread thread0(&ZeroEvenOdd::zero,&obj);
    std::thread thread1(&ZeroEvenOdd::odd,&obj);
    std::thread thread2(&ZeroEvenOdd::even,&obj);
    thread0.join();
    thread1.join();
    thread2.join();
    return 0;
}
```

## Version Works Locally
But it fails on LC
```c++
class ZeroEvenOdd {
private:
    int n;
    int state;  //0 means should print 0, then switch to state 1 or 2 depends on which number is smaller
                //1 means should print odd number, then switch to state 0
                //2 means should print even number, then switch to 0
    int curOdd;
    int curEven;
    std::mutex mtx;

public:
    ZeroEvenOdd(int n) {
        this->n = n;
        this->state=0;
        this->curOdd=1;
        this->curEven=2;
    }

    void printNumber(int x){
        std::cerr<<x;
    }

    // printNumber(x) outputs "x", where x is an integer.
    void zero() {
        while(true){
            mtx.lock();
            if(curOdd>n&&curEven>n){
                mtx.unlock();
                break;
            }
            if(state==0){
                printNumber(0);
                if(curOdd<curEven)
                    state=1;
                else
                    state=2;
            }
            mtx.unlock();
        }
    }

    void odd() {
        while(curOdd<=n){
            mtx.lock();
            // if(curOdd>n){
            //     break;
            //     mtx.unlock();
            // }
            if(state==1){
                printNumber(curOdd);
                state=0;
                curOdd+=2;
            }
            mtx.unlock();
        }
    }

    void even() {
        while(curEven<=n){
            mtx.lock();
            // if(curEven>n){
            //     break;
            //     mtx.unlock();
            // }
            if(state==2){
                printNumber(curEven);
                state=0;
                curEven+=2;
            }
            mtx.unlock();
        }
    }
};
```

## Right Answer
```c++
class ZeroEvenOdd {
private:
    int n;
    std::mutex z,o,e;

public:
    ZeroEvenOdd(int n) {
        this->n = n;
        o.lock();
        e.lock();
    }

    // printNumber(x) outputs "x", where x is an integer.
    void zero(function<void(int)> printNumber) {
        for(int i=1;i<=n;++i){
            z.lock();   // this will cause zero thread lock itself, but other threads will unlock it later. But should we really use mutex like this? This is more like using mutex as a semaphore.
            printNumber(0);
            if(i%2==1)
                o.unlock();
            else
                e.unlock();
        }
    }

    void odd(function<void(int)> printNumber) {
        for(int i=1;i<=n;i+=2){
            o.lock();
            printNumber(i);
            z.unlock();
        }
    }

    void even(function<void(int)> printNumber) {
        for(int i=2;i<=n;i+=2){
            e.lock();
            printNumber(i);
            z.unlock();
        }
    }
};
```