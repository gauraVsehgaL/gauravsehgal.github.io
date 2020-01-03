---
layout: post
title:  "Motivation for compile time if in C++"
date:   2019-11-13 12:58:29
categories: C++
---

```js
#include <iostream>
#include <string>

template<size_t n>
int fibonacci()
{
    return fibonacci<n-1>() + fibonacci<n-2>();
}

template<>
int fibonacci<1>()
{
    return 1;
}

template<>
int fibonacci<2>()
{
    return 1;
}

template<size_t n>
int fibonacciLikeABoss()
{
    if constexpr(n==1)
        return 1;
    else if constexpr(n==2)
        return 1;
    else
       return fibonacciLikeABoss<n-1>() + fibonacciLikeABoss<n-2>();
}

int main()
{
    std::cout<<fibonacciLikeABoss<1>()<<'\n';
    std::cout<<fibonacciLikeABoss<2>()<<'\n';
    std::cout<<fibonacciLikeABoss<3>()<<'\n';
    std::cout<<fibonacciLikeABoss<4>()<<'\n';
    std::cout<<fibonacciLikeABoss<5>()<<'\n';
    std::cout<<fibonacciLikeABoss<6>()<<'\n';
}
```

```js
#include <iostream>
#include <string>

std::string GiveMeAStringFromAnything(std::string astring)
{
    return astring;
}

std::string GiveMeAStringFromAnything(int aint)
{
    return std::to_string(aint);
}

template<typename T>
std::string GiveMeAStringFromAnythingLikeABoss(T somet)
{
    if constexpr(std::is_same_v<T, std::string>)
        return somet;
    else if(std::is_same_v<T, int>)
        return std::to_string(somet);
}

int main()
{
    std::string something = "something";
    std::cout<<GiveMeAStringFromAnythingLikeABoss(something);
    std::cout<<GiveMeAStringFromAnythingLikeABoss(42);
}
```
