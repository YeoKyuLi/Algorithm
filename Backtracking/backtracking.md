# Backtracking

1. Subsets - Medium

   [site](https://leetcode.com/problems/subsets/)

   Given a set of **distinct** integers, *nums*, return all possible subsets (the power set).

   **Note:** The solution set must not contain duplicate subsets.

   **Example:**

   ```
   Input: nums = [1,2,3]
   Output:
   [
     [3],
     [1],
     [2],
     [1,2,3],
     [1,3],
     [2,3],
     [1,2],
     []
   ]
   ```

   ```c++
   // 개선할 부분과 불필요한 부분을 제거하는 연습
   class Solution {
   public:
       vector<vector<int>> subsets(vector<int>& nums) {
           vector<vector<int>> result;
           vector<int> solution;
           sort(nums.begin(), nums.end());
           // for(int sizeOfSolution = 0; sizeOfSolution <= nums.size(); sizeOfSolution++)
           subsets(0, nums, solution, result);
           return result;
       }
   private:
       void subsets(int begin, vector<int>& nums, vector<int>& solution, vector<vector<int>>& result )
       {
           // if(solution.size() == sizeOfSolution)
           // {
           //     // sort(solution.begin(), solution.end());
           //     // if(find(result.begin(), result.end(), solution) == result.end())
           //     result.push_back(solution);
           //     return;
           // }
           result.push_back(solution);
           for(int i = begin ; i < nums.size(); i++)
           {
               solution.push_back(nums[i]);
               subsets(i+1, nums, solution, result);
               solution.pop_back();
           }
           
       }
   };
   ```

2. s

   ```c++
   
   ```

   

3. d

   

   ```c++
   
   ```

   

4. s

   

   ```c++
   
   ```

   

5. s

   

   ```c++
   
   ```

   

6. s

   

   ```c++
   
   ```

   

7. s

   

   ```c++
   
   ```

   