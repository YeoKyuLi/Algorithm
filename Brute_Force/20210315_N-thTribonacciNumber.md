N-th Tribonacci Number
======================

The Tribonacci sequence Tn is defined as follows: 

T0 = 0, T1 = 1, T2 = 1, and Tn+3 = Tn + Tn+1 + Tn+2 for n >= 0.

Given n, return the value of Tn.

 

Example 1:

Input: n = 4
Output: 4
Explanation:
T_3 = 0 + 1 + 1 = 2
T_4 = 1 + 1 + 2 = 4
Example 2:

Input: n = 25
Output: 1389537
 

Constraints:

0 <= n <= 37
The answer is guaranteed to fit within a 32-bit integer, ie. answer <= 2^31 - 1.

![site](https://leetcode.com/problems/n-th-tribonacci-number/)

문제를 읽어보면 Input인 n값이 T_n값을 구한는것이다.
T0 = 0, T1 = 1, T2 = 1 까지는 값이 구해져 있고, 간단하게 재귀로 풀면 가능할것같다.
재귀를 풀때는 if 조건이 중요함으로,,
재귀로 풀거야, dp로 풀수 있지 않을까...? 재귀로 풀고 다른 방법을 더 고안해보자!

T_0 = 0;
T_1 = 1;
T_2 = 1;
T_3 = T_0 + T_1 + T_2
T_4 = T_0 + T_1 + T_2 + T_3;
T_5 = T_0 + T_1 + T_2 + T_3 + T_4;

--> 이렇게 푸니깐 Time Limit Exceeded나온다... 그러면 dp나 다른 array를 이용하는 방법 check...
```c++
class Solution {
public:
    int tribonacci(int n) {
        if(n == 0) return 0;
        else if(n == 1 || n == 2) return 1;
        else return tribonacci(n-3) + tribonacci(n-2) + tribonacci(n-1) ;
    }
};
```

dp를 이용한 방법
```c++
class Solution {
public:
    int tribonacci(int n) {
        vector<int> dp{0,1,1};
        for (int i = 3; i <= n; ++i){
            dp[i % 3] = dp[0] + dp[1] + dp[2];
        }
        return dp[n % 3];
    }
};
```

n == 4인 경우
n = 3
dp = 0, 1, 1
i % 3 = 0
dp[0] = 0 + 1 + 2

n = 4
dp = 2, 1, 1
i % 3 = 1;
dp[1] = 2 + 1 + 1;
pd = 2, 4, 1

return dp[N%3 == 1] = 4;
