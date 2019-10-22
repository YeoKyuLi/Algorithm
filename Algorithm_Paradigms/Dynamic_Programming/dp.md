# Dynamic Programming





* Principles of Dynamic Programming

  1. Tabulation : Bottom up

     It starts its transition from the bottom-most base case dp[0] and reaches its destination state dp[n]. Here, we may notice that the dp table is being populated sequentially and we are directly accessing the calculated states from the table itself and hence, we call it tabulation method.

  ```c++
  //Factorial
  int dp[MAXN];
  
  //base case
  int dp[0] = 1;
  for(int i = 1; i <= n; i++)
    dp[i] = dp[i-1]*i;
  ```

  

  2. Memoization : Top Down

     As we can see we are storing the most recent cache up to a limit so that if next time we got a call from the same state we simply return it from the **memory**.

  ```c++
  //Factorial
  
  // initialized to -1
  int dp[MAXN];
  
  //return fact x!
  int solve(int x)
  {
    if(x==0)
      return 1;
    if(dp[x] != -1)
      return dp[x];
    return (dp[x] = x * solve(x-1));
  }
  ```



* Difference beween Tabulation and Memoization

![tabulation-vs-memoization](https://media.geeksforgeeks.org/wp-content/cdn-uploads/Tabulation-vs-Memoization-1.png)







#### [Overlapping Subproblems Property](https://www.geeksforgeeks.org/dynamic-programming-set-1/)

​		Like Divide and Conquer, Dynamic Programming combines solutions to sub-problems. In dynamic programming, computed solutions to subproblems are stored in a table so that these don't have to be recomputed.

```
                          fib(5)
                     /             \
               fib(4)                fib(3)
             /      \                /     \
         fib(3)      fib(2)         fib(2)    fib(1)
        /     \        /    \       /    \
  fib(2)   fib(1)  fib(1) fib(0) fib(1) fib(0)
  /    \
fib(1) fib(0)
```

​	a. Memoization (Top Down)

​	

```c++
#include<iostream>
#defube NIL -1
#define MAX 100
using namepsace std;

int lookup[MAX];

void init()
{
  int i;
  for(i = 0; i < MAX; i++)
    lookup[i] = NIL;
}

int fib(int n)
{
  if(lookup[n] == NIL)
  {
    if(n <= 1)
      lookup[n] = n;
    else
      lookup[n] = fib(n - 1) + fib(n -2);
  }
  return lookup[n];
}

int main()
{
  int n = 40;
  init();
  cout << fib(n);
  return 0;
}
```

​	b. Tabulation (Bottom Up)



```c++
#include<iostream>
int fib(int n)
{
  int f[n+1];
  int i;
  f[0] = 0; f[1] = 1;
  for(i = 2; i<= n; i++)
    f[i] = f[i-1] + f[i-2];
  
  return f[n];
}
int main()
{
  int n = 9;
  cout << fib(n);
  return 0;
}
```



####[Optimal Substructure Property](https://www.geeksforgeeks.org/dynamic-programming-set-2-optimal-substructure-property/)













