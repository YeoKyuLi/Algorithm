# Combination

1. combination

Given two integers *n* and *k*, return all possible combinations of *k* numbers out of 1 ... *n*.

**Example:**

```
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

```c++
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> output;
        vector<int> tmp(k,0);
        
        combine(n, k, output, tmp);
        return output;
    }
private:
    void combine(int endNum, int len, vector<vector<int>>& output, vector<int>& tmp)
    {
        if(len == 0)
        {
            output.push_back(tmp);
            return;
        }
        for(int i = endNum; i >= 1; i--)
        {
            tmp[len-1]= i;
            combine(i - 1, len - 1, output, tmp);
        }
    }
};
```



2. Combination Sum

   Given a **set** of candidate numbers (`candidates`) **(without duplicates)** and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sums to `target`.

   The **same** repeated number may be chosen from `candidates` unlimited number of times.

   **Note:**

   - All numbers (including `target`) will be positive integers.
   - The solution set must not contain duplicate combinations.

   **Example 1:**

   ```
   Input: candidates = [2,3,6,7], target = 7,
   A solution set is:
   [
     [7],
     [2,2,3]
   ]
   ```

   ```c++
   class Solution {
   public:
       vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
           vector<vector<int>> result;
           vector<int> candi;
           sort(candidates.begin(), candidates.end()); // 값을 계산하기 위한 필요조건
           
           combinationSum(target, candidates, candi, result, 0);
               
           return result;
       }
       
   private:
       void combinationSum(int target, vector<int>& candidates, vector<int>& candi, vector<vector<int>>& result, int begin )
       {
           if(target == 0)
           {
               result.push_back(candi);
               return;
           }
           else if(target < 0) /*&& target >= candidates[i]*/
               return;
           for(int i = begin; i != candidates.size() /*&& target >= candidates[i]*/; i++)
           {
               candi.push_back(candidates[i]);
               combinationSum(target -candidates[i] , candidates, candi, result, i);
               candi.pop_back();
           }
   
       }
   };
   ```

   







3. Combination Sum2

   Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sums to `target`.

   Each number in `candidates` may only be used **once** in the combination.

   **Note:**

   - All numbers (including `target`) will be positive integers.
   - The solution set must not contain duplicate combinations.

   **Example 1:**

   ```
   Input: candidates = [10,1,2,7,6,1,5], target = 8,
   A solution set is:
   [
     [1, 7],
     [1, 2, 5],
     [2, 6],
     [1, 1, 6]
   ]
   ```

   ```c++
   class Solution {
   public:
       vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
           vector<vector<int>> result;
           vector<int> solution;
           sort(candidates.begin(), candidates.end());
           combinationSum2(0, target, candidates, solution, result);
           
           return result;
       }
   private:
       void combinationSum2(int begin, int target, vector<int>& candidates, vector<int>& solution, vector<vector<int>>& result)
       {
           if(target == 0)
           {
               sort(solution.begin(), solution.end());
               if(find(result.begin(), result.end(), solution) == result.end())
                   result.push_back(solution);
               return;
           }
           for(int i = begin; i < candidates.size() && candidates[i] <= target; i++)
           {
               if (i == begin || candidates[i] != candidates[i - 1]){
                   solution.push_back(candidates[i]);
                   combinationSum2(i+1, target - candidates[i], candidates, solution, result);
                   solution.pop_back();
               }
           }
           
       }
   };
   ```

   

4. Combination Sum3

   Find all possible combinations of ***k*** numbers that add up to a number ***n***, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

   **Note:**

   - All numbers will be positive integers.
   - The solution set must not contain duplicate combinations.

   **Example 1:**

   ```
   Input: k = 3, n = 7
   Output: [[1,2,4]]
   ```

   ```c++
   class Solution {
   public:
       vector<vector<int>> combinationSum3(int k, int n) {
           vector<vector<int>> result;
           vector<int> solution;
           combinationSum3(1, k, n, solution, result);
           return result;
       }
   private:
       void combinationSum3(int begin, int len, int target,vector<int>& solution, vector<vector<int>>& result)
       {
           if(target == 0 && len ==0)
           {
               result.push_back(solution);
               return;
           }
           for(int i = begin; i < 10 && target >= i; i++)
           {
               solution.push_back(i);
               combinationSum3(i+1, len-1, target - i, solution, result);
               solution.pop_back();
           }
           
       }
   };
   ```

   

5. Combination Sum4

   Given an integer array with all positive numbers and no duplicates, find the number of possible combinations that add up to a positive integer target.

   **Example:**

   ```
   nums = [1, 2, 3]
   target = 4
   
   The possible combination ways are:
   (1, 1, 1, 1)
   (1, 1, 2)
   (1, 2, 1)
   (1, 3)
   (2, 1, 1)
   (2, 2)
   (3, 1)
   
   Note that different sequences are counted as different combinations.
   
   Therefore the output is 7.
   ```

   ```c++
   class Solution {
   private:
       unordered_map<int, int> map;
   public:
       int combinationSum4(vector<int>& nums, int target) {
           if(nums.empty() || target<0) return 0;
           if(target == 0) return 1;
           if(map.count(target)) return map[target];
           long count = 0;
           for(int i = 0; i < nums.size(); ++i)
               count += combinationSum4(nums, target-nums[i]);
           return map[target] = count;
       }
   };
   ```

   

6. Combination 