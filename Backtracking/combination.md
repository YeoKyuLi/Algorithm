# Combination

1. combinations

   [site](https://leetcode.com/problems/combinations/)

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

   [site](https://leetcode.com/problems/combination-sum/)

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

   [site](https://leetcode.com/problems/combination-sum-ii/)

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

   [site](https://leetcode.com/problems/combination-sum-iii/)

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

   [site](https://leetcode.com/problems/combination-sum-iv/)

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

   

6. Combination - 타켓 넘버

   [OriginalMD](/Users/yeokyuli/Google Drive/KyuLi/구글/Data-Structure/Algorithm Study/20200112.md)

   [site][https://programmers.co.kr/learn/courses/30/lessons/43165]

   ###### 문제 설명

   n개의 음이 아닌 정수가 있습니다. 이 수를 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.

   ```
   -1+1+1+1+1 = 3
   +1-1+1+1+1 = 3
   +1+1-1+1+1 = 3
   +1+1+1-1+1 = 3
   +1+1+1+1-1 = 3
   ```

   사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

   ##### 제한사항

- 주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
- 각 숫자는 1 이상 50 이하인 자연수입니다.
- 타겟 넘버는 1 이상 1000 이하인 자연수입니다.

##### 입출력 예

| numbers         | target | return |
| --------------- | ------ | ------ |
| [1, 1, 1, 1, 1] | 3      | 5      |

##### complexity: t -> O(logN), s->

```c++
#include <string>
#include <vector>
#include <iostream>

using namespace std;

/*
combination
또한 패턴이 중복이 되면 안된당
이것이 그래프 문제인가... 아 그래프로 풀려면 또 그럴순있군..?
이건 DFS로 풀어야지 -> not DFS
*/
void com(int begin, vector<int>& numbers, const int& target, int tmp, int& answer)
{
    if(begin == numbers.size() && target == tmp)
    {
        answer++;
        return;
    }
    // for(int i = begin; i < numbers.size() ; i++)
    if(begin != numbers.size())
    {
        com(begin+1, numbers, target, tmp+numbers[begin], answer);
        com(begin+1, numbers, target, tmp-numbers[begin], answer);
    }
}

int solution(vector<int> numbers, int target) {
    int answer = 0;
    com(0, numbers, target,0, answer);
    return answer;
}
```

7. Letter Combinations of a Phone Number - Medium

   [site](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

   Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent.

   A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

   ![img](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

   **Example:**

   ```
   Input: "23"
   Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
   ```

   **Note:**

   Although the above answer is in lexicographical order, your answer could be in any order you want.

   ```c++
   class Solution {
   public:
       map<string, string> nums= {
           {"2", "abc"},
           {"3", "def"},
           {"4", "ghi"},
           {"5", "jkl"},
           {"6", "mno"},
           {"7", "pqrs"},
           {"8", "tuv"},
           {"9", "wxyz"},
       };
       vector<string> output;
       void combinations(string comb, string next_digits){
           if(next_digits.length() == 0)
               output.push_back(comb);
               // cout << "com : " << comb << endl;
           else{
               string digit = next_digits.substr(0,1);
               string letters = nums.find(digit)->second;
               cout << letters << endl;
               for(int i = 0 ; i < letters.length() ; i++){
                   char letter = letters.at(i);
                   // if(i==0)
                   //     letter = letters.substr(i,i+1);
                   // else
                   //     letter = letters.substr(i,i);
                   cout << letter << endl;
                   combinations(comb+letter, next_digits.substr(1));
               }
           }
          
       }
       vector<string> letterCombinations(string digits) {
           // show content:        
           //숫자에 맞는 값을 Map에서 꺼낸다. 하나씩 보낸다.
           if(digits.length() != 0)
               combinations("", digits);
           
           
           
           // for(int i = 0 ; i < digits.size(); i++){
               
               // cout << nums.find(digits[i])->second << endl;
               //해당 string을 넘겨서 combinations을 만든다.
           
               // combinations("",nums.find(digits[i])->second, nums.find(digits[i])->second.length());
           // }
           
           
           // for (std::map<char, string>::iterator it=nums.begin(); it!=nums.end(); ++it)
           //     std::cout << it->first << " => " << it->second<< '\n';
           
           return output;
       }
   };
   ```

8. c

   ```c++
   
   ```

9. c

   ```c++
   
   ```

10. c

    ```c++
    
    ```

11. c

    ```c++
    
    ```

12. c

    ```c++
    
    ```

    