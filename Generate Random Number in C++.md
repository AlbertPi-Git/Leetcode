# Generate Random Number in C++

## Use C++ uniform_distribution
```c++
std::random_device seedGen;     //true number generator,generate number as the seed of default random engine
std::default_random_engine randGenerator(seedGen());    //instantiate a default random engine

std::uniform_int_distribution<int> rangeIntRand(min,max);   //define uniform integer distribution in [min,max]
std::uniform_real_distribution<double> rangeDbRand(min,max);    //define uniform double distribution in [min,max]

int randInt=rangeIntRand(randGenerator);    //use distribution object and random engine to generate random number
double randDb=rangeDbRand(randGenerator);
```
