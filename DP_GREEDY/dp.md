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



1. Coin Change - Medium

   [site](https://leetcode.com/problems/coin-change/)

   You are given coins of different denominations and a total amount of money *amount*. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

   **Example 1:**

   ```
   Input: coins = [1, 2, 5], amount = 11
   Output: 3 
   Explanation: 11 = 5 + 5 + 1
   ```

   **Example 2:**

   ```
   Input: coins = [2], amount = 3
   Output: -1
   ```

   **Note**:
   You may assume that you have an infinite number of each kind of coin.

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



2. Longest Substring Without Repeating Characters

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



3. Longest Common Prefix(Divide and Conquer)

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



4. Longest Increasing SubSequence (LIS)

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



5. Longest Palindromic Substring

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



6. Word Break - Medium

   [site](https://leetcode.com/problems/word-break/)

   Given a **non-empty** string *s* and a dictionary *wordDict* containing a list of **non-empty** words, determine if *s* can be segmented into a space-separated sequence of one or more dictionary words.

   **Note:**

   - The same word in the dictionary may be reused multiple times in the segmentation.
   - You may assume the dictionary does not contain duplicate words.

   **Example 1:**

   ```
   Input: s = "leetcode", wordDict = ["leet", "code"]
   Output: true
   Explanation: Return true because "leetcode" can be segmented as "leet code".
   ```

   **Example 2:**

   ```
   Input: s = "applepenapple", wordDict = ["apple", "pen"]
   Output: true
   Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
                Note that you are allowed to reuse a dictionary word.
   ```

   **Example 3:**

   ```
   Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
   Output: false
   ```

```c++
class Solution {
public:
    /*
        자르는 구간을 앞에서 부터 -> 그 부분을 조금씩 잘라서 wordDict에 있는지 확인
    */
    bool wordBreak(string s, vector<string>& wordDict) {
        int n = s.length();
        
        vector<bool> dp(n+1, false);
        dp[0] = true; // s is empty.
        
        for(int i = 1 ; i <= n ; i++)
        {
            for(int j = i-1; j >= 0; j--)
            {
                string word = s.substr(j,i-j);
                cout << word << " ";
                if(dp[j]) //dp[j] means can be make words before j(dp is 1 indexed)
                {
                    string word = s.substr(j,i-j);
                    if(find(wordDict.begin(), wordDict.end(), word) != wordDict.end())
                    {
                        dp[i] = true;
                        break;
                    }
                    
                }
            }
            cout << endl;
            
            
        }
        
        for(auto a : dp)
        {
            cout << a << " ";
        }
        
        return dp[n];
    }
};
```



7. Unique Paths - Medium

   [site](https://leetcode.com/problems/unique-paths/)

   A robot is located at the top-left corner of a *m* x *n* grid (marked 'Start' in the diagram below).

   The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

   How many possible unique paths are there?

   ![img](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)
   Above is a 7 x 3 grid. How many possible unique paths are there?

   **Note:** *m* and *n* will be at most 100.

   **Example 1:**

   ```
   Input: m = 3, n = 2
   Output: 3
   Explanation:
   From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
   1. Right -> Right -> Down
   2. Right -> Down -> Right
   3. Down -> Right -> Right
   ```

   **Example 2:**

   ```
   Input: m = 7, n = 3
   Output: 28
   ```

```c++
// Dynamic문제에서 많이 나오는 경로의 수 찾기
// 쉬운측... 하
// 점화식은 어떡해 만들어 줄까
// 초기화 생각해야됨 0x0에서,
// [1,1] = [0,1] + [1,0]
/*

*/
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m, vector<int>(n, 1));
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        return dp[m - 1][n - 1];
    }
    /*
    int uniquePaths(int m, int n) {
        vector<int> cur(n, 1); //  vector v(n,x), v는 x 값으로 초기화된 n개의 원소를 갖는다.
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                cur[j] += cur[j - 1];
            }
        }
        return cur[n - 1];
    }*/
};
```



8. **House Robber** - Easy *****

   [site](https://leetcode.com/problems/house-robber/)

   You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

   Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

   **Example 1:**

   ```
   Input: [1,2,3,1]
   Output: 4
   Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
                Total amount you can rob = 1 + 3 = 4.
   ```

   **Example 2:**

   ```
   Input: [2,7,9,3,1]
   Output: 12
   Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
                Total amount you can rob = 2 + 9 + 1 = 12.
   ```

   ```c++
   class Solution {
   public:
       int rob(vector<int>& nums) {
           //짝수 or 홀수끼리 더해서 큰값 리턴해주면 되는거 아닌가? ==> 실패
           // 나의 앞뒤 빼고는 다 더할 수 있는 대상이 됨. [2,1,1,2] => 4
           // 큰 범위에서 생각해보고, 정리 후 개발 시작하자. 
   
           if(nums.size() == 0 )
               return 0;
           if(nums.size() < 2)
               return nums[0];
           
           vector<int> result(nums.size() , 0);
           if(nums[0] != NULL) result[0] = nums[0];
           if(nums[1] != NULL) result[1] = max(nums[0], nums[1]);
     
   
   //         for(int i = 2 ; i < nums.size(); i++)
   //         {
   //             int maxVal = 0;
   //             for(int j = 0 ;  j < i-1; j++){
   //                 if(i > 2)
   //                     maxVal = max(maxVal,result[j]);
   //                 else
   //                     break;
   //             }
   //             // cout << maxVal ;
   //             result[i] = max(result[i] +  maxVal, result[i]+ result[i-2]);
   
   //         }
           
           
   //         return max(result[result.size()-1], result[result.size()-2]);
           for(int i = 2 ; i < nums.size(); i++)
               result[i] = max(result[i-2] + nums[i], result[i-1]);
           
           return result[nums.size()-1];
           
       }
   };
   
   ```

   

9.  Climbing Stairs

   Easy

   3143103Share

   You are climbing a stair case. It takes *n* steps to reach to the top.

   Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

   **Note:** Given *n* will be a positive integer.

   **Example 1:**

   ```
   Input: 2
   Output: 2
   Explanation: There are two ways to climb to the top.
   1. 1 step + 1 step
   2. 2 steps
   ```

   **Example 2:**

   ```
   Input: 3
   Output: 3
   Explanation: There are three ways to climb to the top.
   1. 1 step + 1 step + 1 step
   2. 1 step + 2 steps
   3. 2 steps + 1 step
   ```

10. **Climbing Stairs** - Easy

    [site](https://leetcode.com/problems/climbing-stairs/)

    You are climbing a stair case. It takes *n* steps to reach to the top.

    Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

    **Note:** Given *n* will be a positive integer.

    **Example 1:**

    ```
    Input: 2
    Output: 2
    Explanation: There are two ways to climb to the top.
    1. 1 step + 1 step
    2. 2 steps
    ```

    **Example 2:**

    ```
    Input: 3
    Output: 3
    Explanation: There are three ways to climb to the top.
    1. 1 step + 1 step + 1 step
    2. 1 step + 2 steps
    3. 2 steps + 1 step
    ```

    ```c++
    /*
    //1 2 3 5
    // f(n) = f(n-1)+f(n-2)
    1. 점화식을 찾는다.
    2. memorization을 고려한다. or recursive
    
    그냥 재귀사용하면 t - O(2^n), s - O(1)
    
    */
    class Solution {
    public:
    // Dynamic Programming
        // int climbStairs(int n) {
        // //solution 1 t - O(n), s - O(N)
        //     vector<int> v(n);
        //     if(n <= 2)
        //         return n;
        //     v[0] = 1;
        //     v[1] = 2;
        //     for(int i = 2; i < n; i++){
        //         v[i] = v[i-1] + v[i-2];
        //     }
        // //solution 2 t - O(N), s - ?
        //     // vector<int> v(n,1);
        //     // v[0] = 1;
        //     // for(int i = 1; i < n; i++){
        //     //     if(i < 3) v[i] += v[i-1];
        //     //     else
        //     //         v[i] = v[i-1] + v[i-2];
        //     // }
        //     return v[n-1];
        // }
    
    // Recursion with Memoization: t - O(2^n), s - O(1)
        int climbStairs(int n)
        {
            vector<int> v(n,1);
            return climbStairs(0, n, v);
        }
    private:
        int climbStairs(int i, int n, vector<int>& v)
        {
            if(i > n)
                return 0;
            if(i == n)
                return 1;
            
            if(v[i] > 1)
                return v[i];
            
            v[i] = climbStairs(i+1, n, v) + climbStairs(i+2, n, v);
            
            return v[i];
        }
    };
    ```

11. Decode Ways - Medium

    [site](https://leetcode.com/problems/decode-ways/)

    A message containing letters from `A-Z` is being encoded to numbers using the following mapping:

    ```
    'A' -> 1
    'B' -> 2
    ...
    'Z' -> 26
    ```

    Given a **non-empty** string containing only digits, determine the total number of ways to decode it.

    **Example 1:**

    ```
    Input: "12"
    Output: 2
    Explanation: It could be decoded as "AB" (1 2) or "L" (12).
    ```

    **Example 2:**

    ```
    Input: "226"
    Output: 3
    Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
    ```

    ```c++
    /*
    1. 알파벳은 1 ~ 26
    2. 숫자를 1 or 2단위로 나뉘어 경우의 수를 구한다. 어떤 방식으로?
    3. dp문제는 점화식을 구한다.
        
    
    t - O(N) / s - O(1)
    */
    class Solution {
    public:
        int numDecodings(string s) {
            
            vector<int> dp(s.length() + 1); // for number 0
            
            // base case
            dp[0] = 1;
            dp[1] = s[0] == '0' ? 0 : 1;
    
            for(int i = 2; i <= s.length(); i++)
            {
                int oneDigit = stoi(s.substr(i-1,1));
                int twoDigit = stoi(s.substr(i-2,2));
                cout << oneDigit << " " << twoDigit << endl;
                if(oneDigit > 0 )
                    dp[i] += dp[i-1];
                
                if(twoDigit >= 10 && twoDigit <= 26)
                    dp[i] += dp[i-2];
            }
    
            return dp[s.length()];
        }
    };
    ```

12. 1463 1로 만들기

    [site](https://www.acmicpc.net/problem/1463)

    | 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
    | :-------- | :---------- | :---- | :---- | :-------- | :-------- |
    | 2 초      | 128 MB      | 93654 | 30725 | 19424     | 31.929%   |

    ## 문제

    정수 X에 사용할 수 있는 연산은 다음과 같이 세 가지 이다.

    1. X가 3으로 나누어 떨어지면, 3으로 나눈다.
    2. X가 2로 나누어 떨어지면, 2로 나눈다.
    3. 1을 뺀다.

    정수 N이 주어졌을 때, 위와 같은 연산 세 개를 적절히 사용해서 1을 만들려고 한다. 연산을 사용하는 횟수의 최솟값을 출력하시오.

    ## 입력

    첫째 줄에 1보다 크거나 같고, 106보다 작거나 같은 정수 N이 주어진다.

    ## 출력

    첫째 줄에 연산을 하는 횟수의 최솟값을 출력한다.

    ## 예제 입력 1 복사

    ```
    2
    ```

    ## 예제 출력 1 복사

    ```
    1
    ```

    ## 예제 입력 2 복사

    ```
    10
    ```

    ## 예제 출력 2 복사

    ```
    3
    ```

    

    ```c++
    //
    //  1로 만들기(1463).cpp
    //  Algorithm_study
    //
    //  Created by Yeo Kyu Li on 31/03/2019.
    //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
    //
    #include <iostream>
    #include <string>
    #include <algorithm>
    using namespace std;
    int main()
    {
        int cnt, i;
        int DP[1000001]{0};
        cin >> cnt;
        for(i = 2; i <= cnt ; i++){
            DP[i] = DP[i-1] + 1;
            if(i % 2 == 0) DP[i] = min(DP[i], DP[i/2]+1);
            if(i % 3 == 0) DP[i] = min(DP[i], DP[i/3]+1);
        }
        
        cout << DP[cnt];
        
        return 0;
    }
    
    ```

13. 9095 - 1, 2, 3 더하기

    [site](https://www.acmicpc.net/problem/9095)

    | 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
    | :-------- | :---------- | :---- | :---- | :-------- | :-------- |
    | 1 초      | 128 MB      | 37779 | 23939 | 16056     | 61.626%   |

    ## 문제

    정수 4를 1, 2, 3의 합으로 나타내는 방법은 총 7가지가 있다. 합을 나타낼 때는 수를 1개 이상 사용해야 한다.

    - 1+1+1+1
    - 1+1+2
    - 1+2+1
    - 2+1+1
    - 2+2
    - 1+3
    - 3+1

    정수 n이 주어졌을 때, n을 1, 2, 3의 합으로 나타내는 방법의 수를 구하는 프로그램을 작성하시오.

    ## 입력

    첫째 줄에 테스트 케이스의 개수 T가 주어진다. 각 테스트 케이스는 한 줄로 이루어져 있고, 정수 n이 주어진다. n은 양수이며 11보다 작다.

    ## 출력

    각 테스트 케이스마다, n을 1, 2, 3의 합으로 나타내는 방법의 수를 출력한다.

    ## 예제 입력 1 복사

    ```
    3
    4
    7
    10
    ```

    ## 예제 출력 1 복사

    ```
    7
    44
    274
    ```

    ```c++
    //
    //  1,2,3 더하기(9095).cpp
    //  Algorithm_study
    //
    //  Created by Yeo Kyu Li on 31/03/2019.
    //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
    //
    #include <iostream>
    
    using namespace std;
    int main()
    {
        int cnt;
        cin >> cnt;
        
        while(cnt--){
            int num;
            int DP[11]{0};
            DP[0] = 1;
    
            cin >> num;
            for(int i = 1 ; i <= num; i++){
                if(i-1 >= 0)
                    DP[i] += DP[i-1];
                if(i-2 >= 0)
                    DP[i] += DP[i-2];
                if(i-3 >= 0)
                    DP[i] += DP[i-3];
            }
            cout << DP[num] << endl;
        }
        
        return 0;
    }
    
    ```

14. 1726 - 2×n 타일링

    [site](https://www.acmicpc.net/problem/11726)

    | 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
    | :-------- | :---------- | :---- | :---- | :-------- | :-------- |
    | 1 초      | 256 MB      | 49886 | 18354 | 13578     | 34.626%   |

    ## 문제

    2×n 크기의 직사각형을 1×2, 2×1 타일로 채우는 방법의 수를 구하는 프로그램을 작성하시오.

    아래 그림은 2×5 크기의 직사각형을 채운 한 가지 방법의 예이다.

    ![img](https://onlinejudgeimages.s3-ap-northeast-1.amazonaws.com/problem/11726/1.png)

    ## 입력

    첫째 줄에 n이 주어진다. (1 ≤ n ≤ 1,000)

    ## 출력

    첫째 줄에 2×n 크기의 직사각형을 채우는 방법의 수를 10,007로 나눈 나머지를 출력한다.

    ## 예제 입력 1 복사

    ```
    2
    ```

    ## 예제 출력 1 복사

    ```
    2
    ```

    ## 예제 입력 2 복사

    ```
    9
    ```

    ## 예제 출력 2 복사

    ```
    55
    ```

    ```c++
    //
    //  2*n 타일링(11726).cpp
    //  Algorithm_study
    //
    //  Created by Yeo Kyu Li on 31/03/2019.
    //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
    //
    #include <iostream>
    using namespace std;
    
    int main()
    {
        int DP[1001]{0};
        
        DP[0] = DP[1] = 1;
        
        int cnt;
        cin >> cnt;
        
        for(int i = 2; i <= cnt; i++){
            DP[i] = (DP[i-1] + DP[i-2]) % 10007;
        }
        
        cout << DP[cnt];
        return 0;
    }
    
    ```

15. 11727 - 2×n 타일링 2

    [site](https://www.acmicpc.net/problem/11727)

    | 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
    | :-------- | :---------- | :---- | :---- | :-------- | :-------- |
    | 1 초      | 256 MB      | 21295 | 12746 | 10187     | 60.008%   |

    ## 문제

    2×n 직사각형을 2×1과 2×2 타일로 채우는 방법의 수를 구하는 프로그램을 작성하시오.

    아래 그림은 2×17 직사각형을 채운 한가지 예이다.

    ![img](https://www.acmicpc.net/upload/images/t2n2122.gif)

    ## 입력

    첫째 줄에 n이 주어진다. (1 ≤ n ≤ 1,000)

    ## 출력

    첫째 줄에 2×n 크기의 직사각형을 채우는 방법의 수를 10,007로 나눈 나머지를 출력한다.

     

    ## 예제 입력 1 복사

    ```
    2
    ```

    ## 예제 출력 1 복사

    ```
    3
    ```

    ## 예제 입력 2 복사

    ```
    8
    ```

    ## 예제 출력 2 복사

    ```
    171
    ```

    ## 예제 입력 3 복사

    ```
    12
    ```

    ## 예제 출력 3 복사

    ```
    2731
    ```

    

    ```c++
    //
    //  2*n 타일링2(11727).cpp
    //  Algorithm_study
    //
    //  Created by Yeo Kyu Li on 31/03/2019.
    //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
    //
    #include <iostream>
    
    using namespace std;
    
    int main()
    {
        int DP[1001]{0};
        int cnt;
        cin >> cnt;
        DP[0] = DP[1] = 1;
        for(int i = 2 ; i <= cnt; i++){
            DP[i] = (DP[i-1] + 2*(DP[i-2]))%10007;
        }
        cout << DP[cnt];
        return 0;
    }
    
    ```

16. s

    ```c++
    
    ```

17. s

    ```c++
    
    ```

18. s

    ```c++
    
    ```

19. s

    ```c++
    
    ```

20. s

    ```c++
    
    ```

    