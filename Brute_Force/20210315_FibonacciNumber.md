Fibonacci Number
===================

![site](https://leetcode.com/problems/fibonacci-number/)

## solution 1
```c++
class Solution {
public:
    int fib(int n) {
        if(n == 0) return 0;
        else if(n == 1) return 1;
        else return fib(n-1) + fib(n-2);
    }
};
```

--> 간소화 할 수 있음.
```c++
class Solution {
public:
    int fib(int n) {
        if( n <= 1)
            return n;
        return fib(n-1) + fib(n-2);
    }
};
```

아래 솔루션은 leetcode에 있는 솔루션임.
기본적으로 재귀를 할때 많이 사용되는 기술들임.
## Approach 2: Bottom-Up Approach using Memoization
아래에서 부터 올라가면서, 내가 계산했던 값을 다시 이용하는 방법임.

```c++
class Solution {
public:
    int fib(int n) {
        if( n <= 1)
            return n;
        return memoize(n);
    }
    
    int memoize(int n)
    {
        vector<int> cache(n+1);
        cache[1] = 1;
        
        for(int i = 2; i <= n; i++)
        {
            cache[i] = cache[i-1] + cache[i-2];
        }
        return cache[n];
    }
};
```

## Approach 3: Top-Down Approach using Memoization
```c++
class Solution {
private:
  int cache[31];
public:
    int fib(int n) {
        if( n <= 1)
            return n;
        cache[0] = 0;
        cache[1] = 1;
        
        for(int i=2;i<31;i++)
            cache[i]=-1;
        
        return memoize(n);
    }
    
    int memoize(int n)
    {
        if(cache[n] != -1)
            return cache[n];
        cache[n] = memoize(n-1) + memoize(n-2);
        
        return memoize(n);
    }
};
```