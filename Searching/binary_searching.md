# Binary Searching

1. Pow(x, n) - Medium

   [site](https://leetcode.com/problems/powx-n/)

   Implement [pow(*x*, *n*)](http://www.cplusplus.com/reference/valarray/pow/), which calculates *x* raised to the power *n* (xn).

   **Example 1:**

   ```
   Input: 2.00000, 10
   Output: 1024.00000
   ```

   **Example 2:**

   ```
   Input: 2.10000, 3
   Output: 9.26100
   ```

   **Example 3:**

   ```
   Input: 2.00000, -2
   Output: 0.25000
   Explanation: 2-2 = 1/22 = 1/4 = 0.25
   ```

   **Note:**

   - -100.0 < *x* < 100.0
   - *n* is a 32-bit signed integer, within the range [−231, 231 − 1]

   ```c++
   class Solution {
   public:
       double myPow(double x, int n) {
           /*
           0. n < 0 ==> 1 / (x ^ -n)
           1. n ==0 -> 1
           2. n == 1 -> x
           3. x ^ n = (x ^ (n/2)) *  (x ^ (n/2))
           4. x ^ n = x *( x ^ (n-1))
           myPow(2,10)
           n = 5 (x*x) * (x*x) * x
           n = 4 (x*x) * (x*x)
           n = 2 x * x
           n = 1 x
           
           time - O(logN)
               n % 2하는 부분이 있기때문에 횟수가 줄어들어서 logN일것 같다.
           space - O(logN)
               recursive가 들어가기 때문에
           */
           if( n == 0) return 1;
           if(n == INT_MIN) return myPow(x, n/2);
           if(n < 0 ) return 1 / myPow(x, -n);
           if(n % 2 == 0)
           {
               double temp = myPow(x, n/2);
               return temp * temp;
           }
           else
               return x*myPow(x, n-1);
           
       }
   };
   ```

   

2. Longest Increasing Subsequence - Medium

   [site](https://leetcode.com/problems/longest-increasing-subsequence/)

   Given an unsorted array of integers, find the length of longest increasing subsequence.

   **Example:**

   ```
   Input: [10,9,2,5,3,7,101,18]
   Output: 4 
   Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
   ```

   **Note:**

   - There may be more than one LIS combination, it is only necessary for you to return the length.
   - Your algorithm should run in O(*n2*) complexity.

   **Follow up:** Could you improve it to O(*n* log *n*) time complexity?

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

3. Kth Smallest Element in a Sorted Matrix - Medium

   [site](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)

   Given a *n* x *n* matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

   Note that it is the kth smallest element in the sorted order, not the kth distinct element.

   **Example:**

   ```
   matrix = [
      [ 1,  5,  9],
      [10, 11, 13],
      [12, 13, 15]
   ],
   k = 8,
   
   return 13.
   ```

   

   **Note:**
   You may assume k is always valid, 1 ≤ k ≤ n2.

   ```c++
   class Solution {
   public:
       int kthSmallest(vector<vector<int>>& matrix, int k) {
           int count = 1;
           
           vector<int> copy;
           for(vector s : matrix)
           {
               for(int i = 0; i < s.size();i++)
                   copy.push_back(s[i]);
           }
           
           sort(copy.begin(), copy.end());
           for(int i = 0 ; i < copy.size(); i++)
           {
               return copy.at(k-1);
           }
           
           return -1;
       }
   };
   ```

4. Kth Smallest Element in a BST - Medium

   [site](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

   Given a binary search tree, write a function `kthSmallest` to find the **k**th smallest element in it.

   **Note:**
   You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

   **Example 1:**

   ```
   Input: root = [3,1,4,null,2], k = 1
      3
     / \
    1   4
     \
      2
   Output: 1
   ```

   **Example 2:**

   ```
   Input: root = [5,3,6,2,4,null,null,1], k = 3
          5
         / \
        3   6
       / \
      2   4
     /
    1
   Output: 3
   ```

   **Follow up:**
   What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?

   ```c++
   /**
    * Definition for a binary tree node.
    * struct TreeNode {
    *     int val;
    *     TreeNode *left;
    *     TreeNode *right;
    *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
    * };
    */
   class Solution {
   public:
       vector<int> v;
       vector<int> traversal(TreeNode* head)
       {
           if(head == NULL) return v;
           traversal(head->left);
           v.push_back(head->val);
           traversal(head->right);
           return v;
       }
       int kthSmallest(TreeNode* root, int k) {
           traversal(root);
           cout << v.at(k-1) << endl;
           for(int x : v)
               cout << x << " ";
           
           return v.at(k-1);
       }
   };
   ```

5. Divide Two Integers - Medium

   [site](https://leetcode.com/problems/divide-two-integers/)

   Given two integers `dividend` and `divisor`, divide two integers without using multiplication, division and mod operator.

   Return the quotient after dividing `dividend` by `divisor`.

   The integer division should truncate toward zero.

   **Example 1:**

   ```
   Input: dividend = 10, divisor = 3
   Output: 3
   ```

   **Example 2:**

   ```
   Input: dividend = 7, divisor = -3
   Output: -2
   ```

   **Note:**

   - Both dividend and divisor will be 32-bit signed integers.
   - The divisor will never be 0.
   - Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 231 − 1 when the division result overflows.

   ```c++
   class Solution {
   public:
       int divide(int dividend, int divisor) {
           if (dividend == INT_MIN && divisor == -1) {
               return INT_MAX;
           }
           long result = 0;
           int sign = dividend > 0 ^ divisor > 0 ? -1 : 1;
           long dvd = labs(dividend), div = labs(divisor);
   
           
           while(dvd >= div)
           {
               long tmp = div, m = 1;
               while(tmp << 1 <= dvd) // right shift를 하면 *2, left shift 하면 /2
               {
                   tmp <<= 1;
                   m <<= 1;
               }
               dvd -= tmp;
               result += m;
           }
           
           // while(dvd >= div)
           // {
           //     dvd -= div;
           //     result++;
           // }
           
           return sign * result;
           
       }
   };
   ```

6. 1920 - 수 찾기

   [site](https://www.acmicpc.net/problem/1920)

   | 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
   | :-------- | :---------- | :---- | :---- | :-------- | :-------- |
   | 2 초      | 128 MB      | 44369 | 12241 | 7959      | 28.039%   |

   ## 문제

   N개의 정수 A[1], A[2], …, A[N]이 주어져 있을 때, 이 안에 X라는 정수가 존재하는지 알아내는 프로그램을 작성하시오.

   ## 입력

   첫째 줄에 자연수 N(1≤N≤100,000)이 주어진다. 다음 줄에는 N개의 정수 A[1], A[2], …, A[N]이 주어진다. 다음 줄에는 M(1≤M≤100,000)이 주어진다. 다음 줄에는 M개의 수들이 주어지는데, 이 수들이 A안에 존재하는지 알아내면 된다. 모든 정수들의 범위는 int 로 한다.

   ## 출력

   M개의 줄에 답을 출력한다. 존재하면 1을, 존재하지 않으면 0을 출력한다.

   ## 예제 입력 1 복사

   ```
   5
   4 1 5 2 3
   5
   1 3 7 9 5
   ```

   ## 예제 출력 1 복사

   ```
   1
   1
   0
   0
   1
   ```

   ```c++
   //
   //  수 찾기 (1920).cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 21/05/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   
   #include <iostream>
   #include <vector>
   #include <algorithm>
   using namespace std;
   int N, M;
   vector<int> v(N);
   int BinarySearch(int low, int high, int target){
       if(low > high)
           return 0;
       else{
           int mid = (low+high)/2;
           if(v[mid] == target)
               return 1;
           else if(v[mid] > target)
               return BinarySearch(low, mid-1, target);
           else
               return BinarySearch(mid+1, high, target);
       }
   }
   
   int main()
   {
       ios_base::sync_with_stdio();
       cin.tie(0);
       cout.tie(0);
       
       cin >> N;
       
       for(int i = 0 ; i < N; i++){
           int k;
           cin >> k;
           v.push_back(k);
       }
       
       // need to sorting for using binaray serach
       sort(v.begin(), v.end());
       
       cin >> M;
       for(int j = 0; j < M; j++){
           int num;
           cin >> num;
           cout << BinarySearch(0, N-1, num) << "\n";
   
       }
       //        for(int j = 0 ; j < N ; j++){
       //            if(num == v[j]){
       //                cout << "1" << endl;
       //                break;
       //            }
       //            else if(j == N-1)
       //                cout << "0" << endl;
       //        }
       return 0;
   }
   
   ```

7. s

   ```c++
   
   ```

8. s

   ```c++
   
   ```

   