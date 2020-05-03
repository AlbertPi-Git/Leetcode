# Leetcode 1195 - FizzBuzz

## Initial Idea
Only use mutex.

This is not really synchronizing, just let them compete for the lock. Only when the right thread get the lock, it will increment i. Apparently this is inefficient.
```c++
class FizzBuzz {
private:
    int n;
    int i;
    std::mutex mtx;

public:
    FizzBuzz(int n) {
        this->n = n;
        this->i=1;
    }

    // printFizz() outputs "fizz".
    void fizz(function<void()> printFizz) {
        while(true){
            mtx.lock();
            if(i>n){
                mtx.unlock();
                break;
            }
            if(i%3==0&&i%5!=0){
                printFizz();
                ++i;
            }
            mtx.unlock();
        }
    }

    // printBuzz() outputs "buzz".
    void buzz(function<void()> printBuzz) {
        while(true){
            mtx.lock();
            if(i>n){
                mtx.unlock();
                break;
            }
            if(i%3!=0&&i%5==0){
                printBuzz();
                ++i;
            }
            mtx.unlock();
        }
    }

    // printFizzBuzz() outputs "fizzbuzz".
	void fizzbuzz(function<void()> printFizzBuzz) {
        while(true){
            mtx.lock();
            if(i>n){
                mtx.unlock();
                break;
            }
            if(i%3==0&&i%5==0){
                printFizzBuzz();
                ++i;
            }
            mtx.unlock();
        }
    }

    // printNumber(x) outputs "x", where x is an integer.
    void number(function<void(int)> printNumber) {
        while(true){
            mtx.lock();
            if(i>n){
                mtx.unlock();
                break;
            }
            if(i%3!=0&&i%5!=0){
                printNumber(i);
                ++i;
            }
            mtx.unlock();
        }
    }
};
```

## Others' Idea 1
Only use mutex.

Use mutex as semaphore to do synchronizing (sounds strange, but functionally this is like using mutex as semaphore. Even if in c++ the a thread that already owns mutex locks mutex again is undefined behavior.)
```c++
class FizzBuzz {
private:
    int n;
    std::mutex fizzL,buzzL,fizzbuzzL,numL;

public:
    FizzBuzz(int n) {
        this->n = n;
        fizzL.lock();
        buzzL.lock();
        fizzbuzzL.lock();
    }

    // printFizz() outputs "fizz".
    void fizz(function<void()> printFizz) {
        for(int i=3;i<=n;i+=3){
            if(i%5!=0){
                fizzL.lock();
                printFizz();
                numL.unlock();
            }
        }

    }

    // void fizz(function<void()> printFizz) {
    //     for(int i=3;i<=n;i+=3){
    //         fizzL.lock();    //this is wrong version, since number() will only unlock fizzL when i%3==0&&i!=5. Thus, when i==15, fizzL is locked and lock() is called again, which cause deadlock.
    //         if(i%5!=0)
    //             printFizz();
    //         numL.unlock();
    //     }

    // }

    // printBuzz() outputs "buzz".
    void buzz(function<void()> printBuzz) {
        for(int i=5;i<=n;i+=5){
            if(i%3!=0){
                buzzL.lock();
                printBuzz();
                numL.unlock();
            }
        }
    }

    // void buzz(function<void()> printBuzz) {
    //     for(int i=5;i<=n;i+=5){
    //         buzzL.lock();
    //         if(i%3!=0)
    //             printBuzz();
    //         numL.unlock();
    //     }
    // }

    // printFizzBuzz() outputs "fizzbuzz".
	void fizzbuzz(function<void()> printFizzBuzz) {
        for(int i=15;i<=n;i+=15){
            fizzbuzzL.lock();
            printFizzBuzz();
            numL.unlock();
        }
    }

    // printNumber(x) outputs "x", where x is an integer.
    void number(function<void(int)> printNumber) {
        for(int i=1;i<=n;++i){
            numL.lock();
            if(i%3==0&&i%5!=0)
                fizzL.unlock();
            else if(i%3!=0&&i%5==0)
                buzzL.unlock();
            else if(i%3==0&&i%5==0)
                fizzbuzzL.unlock();
            else{
                printNumber(i);
                numL.unlock();
            }
        }
    }
};
```