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

​	Optimal solution of the given problem can be obtained by using optimal solutions of its subproblems. The Shortest Path problem has following optimal substructure property. The standard All Pair Shortest Path algorithms like **Floyd-Warshall** and **Bellman-Ford** are typical examples of Dynamic Programming.



* **Frequently Problems**
  * [Coin change problem](https://www.geeksforgeeks.org/dynamic-programming-set-7-coin-change/)
  * [Longest Common Subsequence](https://www.geeksforgeeks.org/longest-common-subsequence/)
  * [Longest Repeated Subsequence](https://www.geeksforgeeks.org/longest-repeated-subsequence/)
  * [Longest Increasing Subsequence](https://www.geeksforgeeks.org/longest-increasing-subsequence/)
  * [A Space Optimized Solution of LCS](https://www.geeksforgeeks.org/space-optimized-solution-lcs/)
  * [LCS (Longest Common Subsequence) of three strings](https://www.geeksforgeeks.org/lcs-longest-common-subsequence-three-strings/)
  * [Longest subsequence such that difference between adjacents is one](https://www.geeksforgeeks.org/longest-subsequence-such-that-difference-between-adjacents-is-one/)
  * [Maximum length subsequence with difference between adjacent elements as either 0 or 1](https://www.geeksforgeeks.org/maximum-length-subsequence-difference-adjacent-elements-either-0-1/)
  * [Maximum sum increasing subsequence from a prefix and a given element after prefix is must](https://www.geeksforgeeks.org/maximum-sum-increasing-subsequence-from-a-prefix-and-a-given-element-after-prefix-is-must/)
  * [Floyd Warshall Algorithm](https://www.geeksforgeeks.org/dynamic-programming-set-16-floyd-warshall-algorithm/)
  * [Bellman–Ford Algorithm](https://www.geeksforgeeks.org/dynamic-programming-set-23-bellman-ford-algorithm/)
  * [Longest Palindromic Substring | Set 1](https://www.geeksforgeeks.org/longest-palindrome-substring-set-1/)
  * [Longest Palindromic Subsequence](https://www.geeksforgeeks.org/dynamic-programming-set-12-longest-palindromic-subsequence/)
  * [Shortest Common Supersequence](https://www.geeksforgeeks.org/shortest-common-supersequence/)
  * [Longest alternating subsequence](https://www.geeksforgeeks.org/longest-alternating-subsequence/)
  * [Shortest Uncommon Subsequence](https://www.geeksforgeeks.org/shortest-uncommon-subsequence/)
  * [Longest Repeating Subsequence](https://www.geeksforgeeks.org/longest-repeating-subsequence/)
  * [Longest Common Increasing Subsequence (LCS + LIS)](https://www.geeksforgeeks.org/longest-common-increasing-subsequence-lcs-lis/)
  * [Optimal Binary Search Tree](https://www.geeksforgeeks.org/dynamic-programming-set-24-optimal-binary-search-tree/)
  * [Palindrome Partitioning](https://www.geeksforgeeks.org/dynamic-programming-set-17-palindrome-partitioning/)
  * [Longest Arithmetic Progression](https://www.geeksforgeeks.org/length-of-the-longest-arithmatic-progression-in-a-sorted-array/)
  * [Longest Geometric Progression](https://www.geeksforgeeks.org/longest-geometric-progression/)
  * [Top 20 Dynamic Programming Interview Questions](https://www.geeksforgeeks.org/top-20-dynamic-programming-interview-questions/)



* Coin Chnage

```c++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        if(amount == 0)
            return 0;
        
        vector<int> dp(amount+1, amount+1); // initialnazation 12
        
        dp[0] = 0;

        for(int i = 1; i <= amount; i++)
        {
            for(int j = 0 ; j < coins.size(); j++)
            {
                if(coins[j] <= i){
                    cout << dp[i] << " " << dp[i - coins[j]] + 1  << " " << coins[j]<< endl;
                    dp[i] = min(dp[i], dp[i - coins[j]] + 1);
                }
            }
        }
        return dp[amount] > amount ? -1 : dp[amount];
        
    }
    
};
```



* Longest Substring Without Repeating Characters

  ```c++
  #include <iostream>
  #include <string>
  #include <unordered_set>
  using namespace std;
  class Solution {
  public:
      //Sliding Window
      int lengthOfLongestSubstring(string s) {
          int n = s.length(); // s.size();
          unordered_set<int> set;
          int i =0, j =0, max_sub = 0;
  
          while(i < n && j < n){
              if(set.find(s[j]) == set.end()){
                  set.insert(s[j++]);
                  max_sub = max(max_sub, j - i);
              }
              else{
                  set.erase(s[i++]);
              }                
          }
  //         unordered_set<int> :: iterator itr;
  //         for(itr = set.begin() ; itr != set.end() ;itr++){
  //             cout << (char)*itr << endl;
  //         }
          
          return max_sub;
      }
  };
  ```

  

* Longest Common Prefix(Divide and Conquer)

```c++
#include <algorithm>
#include <string>
using namespace std;
class Solution {
public:
    //Divide and Conquer
    string longestCommonPrefix(vector<string>& strs) {
        
        if(strs.size() == 0) return "";
        return longestCommonPrefix(strs, 0, strs.size()-1);
    }
    
    string longestCommonPrefix(vector<string>& strs, int l, int r)
    {
        if(l == r)
            return strs[r];
        else
        {
            int mid = (l+r)/2;
            cout << l << " " << r << endl;
            string leftSub = longestCommonPrefix(strs, l, mid);
            string rightSub = longestCommonPrefix(strs, mid+1, r);
            return commonPrefix(leftSub, rightSub);
        }
    }
    
    string commonPrefix(string left, string right)
    {
        int min = std::min(left.length(), right.length());
        cout << left << " " << right << endl;
        
        for(int i = 0 ; i < min; i ++){
            if(left[i] != right[i])
                return right.substr(0, i);
            
        }
        return right.substr(0, min);
    }
};
```



* Longest Increasing SubSequence (LIS)

  ```c++
  #include <algorithm>
  class Solution {
  public:
      // DP
      int lengthOfLIS(vector<int>& nums) {
          if(nums.size() == 0)
              return 0;
          
          vector<int> dp(nums.size() , 1);
          dp[0] = 1;
          int res = 1;
          
          for(int i = 1; i < nums.size(); i++)
          {
              for(int j = 0 ; j < i; j++)
              {
                  if(nums[i] > nums[j]){
                      dp[i] = max(dp[i], dp[j]+1);
                  }
              }
              
              res = max (res, dp[i]);
          }
          return res;
      }
  };
  ```

  

  ```c++
  class Solution {
  public:
      //Binary Search
      int lengthOfLIS(vector<int>& nums) {
          vector<int>dp;
          for(int x: nums){
              int pos = lower_bound(dp.begin(), dp.end(), x) - dp.begin();
              cout << pos << " " << x << endl;
              if(pos == dp.size()) dp.push_back(x);
              else dp[pos] = x;
          }
          cout << endl;
          for(int x : dp)
              cout << x << " ";
          return dp.size();
      }
  };
  ```

  

* Longest Palindromic Substring

  ```c++
  class Solution {
      //Manacher's Algorithm https://junis3.tistory.com/15
      // https://algospot.com/wiki/read/Manacher's_algorithm
      public: 
      string init(string s){  
          string k = "$#";
          for(int i = 0 ; i < s.size(); i++){
              k += (s[i]);
              k += ('#');
          }
          return k;
      }
      
      string longestPalindrome(string s) {
          string str = init(s);
          string result;
          int r, k, cntMax, position;
          int R[str.size()]={0};
          r = k = cntMax = -1;
  
          for(int i = 0 ; i < str.size(); i++){
              if(i>r) R[i] = 0;
              if(i<=r) R[i] = min(r-i, R[2*k-i]); // k를 기준으로, 대칭점 구하는 것 R[2*k-i]
              
              // S[i−p[i]−1]=S[i+p[i]+1]가 성립하지 않을 때까지 p[i]++
              while(i-R[i]-1 >= 0 and i+R[i]+1 < str.size() and str[i-R[i]-1] == str [i+R[i]+1] ) R[i]++;
              if(r < i + R[i]) r = i+R[i], k=i;
              // R[i]에서의 max를 구하는것!
              if(cntMax <= R[i]){
                  cntMax = R[i];
                  position = i;
              }
          }
   
          int start = (position  - 1 - cntMax)/2;
          int end = (position + cntMax - 1)/2;
    
          for(int i = start ; i < end;i++){
              result += s[i];
          }
          return result;
      }
  };
  ```

  

* 

* d

  





