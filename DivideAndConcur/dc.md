# Divide and Concur

1. Maximum Subarray - Easy

   [site](https://leetcode.com/problems/maximum-subarray/)

   Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

   **Example:**

   ```
   Input: [-2,1,-3,4,-1,2,1,-5,4],
   Output: 6
   Explanation: [4,-1,2,1] has the largest sum = 6.
   ```

   **Follow up:**

   If you have figured out the O(*n*) solution, try coding another solution using the divide and conquer approach, which is more subtle.

   ```c++
   class Solution {
   public:
       int maxSubArray(vector<int>& nums) {
           auto max_sum = INT_MIN, sum = 0;
           for (auto n : nums)
           {
               sum = max(n, sum + n);
               max_sum = max(max_sum, sum);
           }
   
           return max_sum;
       } 
   };
   ```

   

2. s

   

   ```c++
   
   ```

   

3. 

   ```c++
   
   ```

   