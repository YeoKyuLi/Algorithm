# Array

1. Arrary -  Find Peak Element

   [Original MD](/Users/yeokyuli/Google Drive/KyuLi/구글/Data-Structure/Algorithm Study/20200112.md)

   [site](https://leetcode.com/problems/find-peak-element/)

   A peak element is an element that is greater than its neighbors.

   Given an input array `nums`, where `nums[i] ≠ nums[i+1]`, find a peak element and return its index.

   The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

   You may imagine that `nums[-1] = nums[n] = -∞`.

   ```c++
   class Solution {
   public:
       /*
       왼쪽 오른쪽보다 큰 수 찾기, 각 끝자리는 -> 한 쪽만 커도 인정?
       아니면 그냥 max값만 찾아도 성공?
       */
       int findPeakElement(vector<int>& nums) {
           int result;
           for(int i = 1 ; i < nums.size(); i++)
           {
               if(nums[i-1] < nums[i]) // 오른쪽이 클경우
               {
                   if(i == nums.size()-1 || nums[i] > nums[i+1])
                   {
                       result = i;
                       break;
                   }
               }
               else
               {
                   if((i-1) == 0)
                   {
                       result= i-1;
                       break;
                   }
                   
               }
           }
           return result;
       }
   };
   ```

   

2. Array - Word Search (Medium)

   [Site](https://leetcode.com/problems/word-search/)

   Given a 2D board and a word, find if the word exists in the grid.

   The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

   **Example:**

   ```
   board =
   [
     ['A','B','C','E'],
     ['S','F','C','S'],
     ['A','D','E','E']
   ]
   
   Given word = "ABCCED", return true.
   Given word = "SEE", return true.
   Given word = "ABCB", return false.s
   ```

   ```c++
   class Solution {
   public:
       // t - O(N), s - ?
       bool exist(vector<vector<char>>& board, string word) {
           // sort(board.begin(), board.end(),[](const vector<int>& left, const vector<int>& right)
           // {
           //     return left[0] < right[0];
           // });
           if(word.size() == 0 || board.size() == 0)
               return true;
   
           for(int i = 0 ; i < board.size(); i++)
           {
               for(int j = 0; j < board[i].size(); j++)
               {
                   
                   if(board[i][j] == word[0] && dfs(board, word, i, j))
                       return true;
                   
                   // if(find(word.begin(), word.end(), board[i][j]) != word.end())
                   // {
                   //     cout << word.at(word.find(board[i][j])) << " ";
                   //     word.erase(word.find(board[i][j]), 1);
                   //     // word.erase(remove(word.begin(), word.end(), board[i][j]), word.end());
                   //     // remove_copy(word.begin(), word.end(), word.begin(), board[i][j]);
                   // }
                   
               }
           }
           
           return false;
       }
   private:
       bool dfs(vector<vector<char>>& board, string word, int x, int y)
       {
           if(word.length() == 0)
               return true;
           if(x < 0 || y < 0 || x >= board.size() || y >= board[0].size() || board[x][y] != word[0]) 
               return false;
           // if(board[x][y] == word[0])
           // {
           char c = word[0];
           board[x][y] = '\0';
           if(dfs(board, word.substr(1), x+1, y) ||
              dfs(board, word.substr(1), x-1, y) ||
              dfs(board, word.substr(1), x, y+1) ||
              dfs(board, word.substr(1), x, y-1) )
               return true;
           board[x][y] = c;
               
           // }
           return false;
           
       }
   };
   ```

   

3. spiral matrix - Medium

   [site](https://leetcode.com/problems/spiral-matrix/)

   Given a matrix of *m* x *n* elements (*m* rows, *n* columns), return all elements of the matrix in spiral order.

   **Example 1:**

   ```
   Input:
   [
    [ 1, 2, 3 ],
    [ 4, 5, 6 ],
    [ 7, 8, 9 ]
   ]
   Output: [1,2,3,6,9,8,7,4,5]
   ```

   **Example 2:**

   ```
   Input:
   [
     [1, 2, 3, 4],
     [5, 6, 7, 8],
     [9,10,11,12]
   ]
   Output: [1,2,3,4,8,12,11,10,9,5,6,7]
   ```

   ```c++
   class Solution {
   public:
       vector<int> spiralOrder(vector<vector<int>>& matrix) {
           vector<int> result;
           if(matrix.size() == 0)
               return result;
           int x = 0, x2 = matrix.size()-1;
           int y = 0, y2 = matrix[0].size()-1;
           
           while(x <= x2 && y <= y2)
           {
               for(int i = y; i <= y2; i++) result.push_back(matrix[x][i]);
               for(int j = x+1; j <= x2; j++) result.push_back(matrix[j][y2]);
               if(x < x2)
                   for(int a = y2 -1 ; a > y; a--) result.push_back(matrix[x2][a]);
               if(y < y2)
                   for(int b = x2; b > x; b--) result.push_back(matrix[b][y]);
               x++,x2--,y++,y2--;
           }
           return result;
       }
   };
   
   ```

4. Rotate image - Medium

   [site](https://leetcode.com/problems/rotate-image/)

   You are given an *n* x *n* 2D matrix representing an image.

   Rotate the image by 90 degrees (clockwise).

   **Note:**

   You have to rotate the image [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm), which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

   **Example 1:**

   ```
   Given input matrix = 
   [
     [1,2,3],
     [4,5,6],
     [7,8,9]
   ],
   
   rotate the input matrix in-place such that it becomes:
   [
     [7,4,1],
     [8,5,2],
     [9,6,3]
   ]
   ```

   **Example 2:**

   ```
   Given input matrix =
   [
     [ 5, 1, 9,11],
     [ 2, 4, 8,10],
     [13, 3, 6, 7],
     [15,14,12,16]
   ], 
   
   rotate the input matrix in-place such that it becomes:
   [
     [15,13, 2, 5],
     [14, 3, 4, 1],
     [12, 6, 8, 9],
     [16, 7,10,11]
   ]
   ```

   ```c++
   class Solution {
   public:
       void rotate(vector<vector<int>>& matrix) {
           int s = matrix.size()-1;
           int a = 0;
           while(s>a)
           {
               for(int i = 0 ; i < (s-a); i++)
               {
                   swap(matrix[a][a+i], matrix[a+i][s]);
                   swap(matrix[a][a+i], matrix[s][s-i]);
                   swap(matrix[a][a+i], matrix[s-i][a]);
               }
               s--;
               a++;
           }
       }
   };
   ```

   

5. Remove Duplicates from Sorted Array - Esay

   [site](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

   Given a sorted array *nums*, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each element appear only *once* and return the new length.

   Do not allocate extra space for another array, you must do this by **modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** with O(1) extra memory.

   **Example 1:**

   ```
   Given nums = [1,1,2],
   
   Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
   
   It doesn't matter what you leave beyond the returned length.
   ```

   **Example 2:**

   ```
   Given nums = [0,0,1,1,1,2,2,3,3,4],
   
   Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.
   
   It doesn't matter what values are set beyond the returned length.
   ```

   **Clarification:**

   Confused why the returned value is an integer but your answer is an array?

   Note that the input array is passed in by **reference**, which means modification to the input array will be known to the caller as well.

   Internally you can think of this:

   ```
   // nums is passed in by reference. (i.e., without making a copy)
   int len = removeDuplicates(nums);
   
   // any modification to nums in your function would be known by the caller.
   // using the length returned by your function, it prints the first len elements.
   for (int i = 0; i < len; i++) {
       print(nums[i]);
   }
   ```

   ```c++
   class Solution {
   public:
       int removeDuplicates(vector<int>& nums) {
           int result = 0;
           
           if(nums.size() == 0)
               return result;
           
           
           sort(nums.begin(), nums.end());
           for(int i = 1 ; i < nums.size(); i++)
           {
               if(nums[i] != nums[result]){
                   result++;
                   nums[result] = nums[i];
               }
               
           }
           
           return result+1;
           
       }
   };
   ```

6. Plus One - easy

   [site](https://leetcode.com/problems/plus-one/)

   Given a **non-empty** array of digits representing a non-negative integer, plus one to the integer.

   The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

   You may assume the integer does not contain any leading zero, except the number 0 itself.

   **Example 1:**

   ```
   Input: [1,2,3]
   Output: [1,2,4]
   Explanation: The array represents the integer 123.
   ```

   **Example 2:**

   ```
   Input: [4,3,2,1]
   Output: [4,3,2,2]
   Explanation: The array represents the integer 4321.
   ```

   ```c++
   /*
   1. 배열의 뒤부터 계산한다.
   2. 더했을때 10이 아니면 마지막 값 더한걸로 return
   3. 10이 넘으면, 10이 넘지 않는곳까지 계속 계산,
   t - o(N), s-(1)
   */
   class Solution {
   public:
       vector<int> plusOne(vector<int>& digits) {
           
           if(digits.size() == 0)
               return digits;
      
           for(int i = digits.size()-1; i >= 0; i--)
           {
               int plusOne = digits[i]+1;
               if(plusOne < 10){
                   digits[i] = plusOne;
                   return digits;
               }
               // digits[i] = 0;
   
               digits[i] = plusOne % 10;
   
           }
           vector<int> res(digits.size()+1);
           res[0]= 1;
           
   
           
           return res;
       }
   };
   ```

7. Merge Sorted Array - Esay

   Given two sorted integer arrays *nums1* and *nums2*, merge *nums2* into *nums1* as one sorted array.

   **Note:**

   - The number of elements initialized in *nums1* and *nums2* are *m* and *n* respectively.
   - You may assume that *nums1* has enough space (size that is greater or equal to *m* + *n*) to hold additional elements from *nums2*.

   **Example:**

   ```
   Input:
   nums1 = [1,2,3,0,0,0], m = 3
   nums2 = [2,5,6],       n = 3
   
   Output: [1,2,2,3,5,6]
   ```

   ```c++
   class Solution {
   public:
       
       void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
           for(int i=m; i<m+n; i++){
               nums1[i]=nums2[i-m];
            }
       
           std::sort(nums1.begin(), nums1.end());     
       }
   };
   ```

8. Merge Intervals - Medium

   Given a collection of intervals, merge all overlapping intervals.

   **Example 1:**

   ```
   Input: [[1,3],[2,6],[8,10],[15,18]]
   Output: [[1,6],[8,10],[15,18]]
   Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
   ```

   **Example 2:**

   ```
   Input: [[1,4],[4,5]]
   Output: [[1,5]]
   Explanation: Intervals [1,4] and [4,5] are considered overlapping.
   ```

   **NOTE:** input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.

   ```c++
   
   class Solution {
   public:
   
       vector<vector<int>> merge(vector<vector<int>>& intervals) {
           vector<vector<int>> result;
           if(intervals.empty())
               return result;
           
           // sort(intervals.begin(), intervals.end(), [](const vector<int>& left, const vector<int>& right)
           // {
           //     return left[0] < right[0];
           // });
           sort(intervals.begin(), intervals.end());
           result.push_back(intervals[0]);
           for(int i = 1 ; i < intervals.size(); i++)
           {
               if(result.back()[1] < intervals[i][0])
                   result.push_back(intervals[i]);
               else
                   result.back()[1] = max(result.back()[1], intervals[i][1]);
           }
           return result;
       }
   };
   
   
   ```

9. majority element - Easy

   [site](https://leetcode.com/problems/majority-element/)

   Given an array of size *n*, find the majority element. The majority element is the element that appears **more than** `⌊ n/2 ⌋` times.

   You may assume that the array is non-empty and the majority element always exist in the array.

   **Example 1:**

   ```
   Input: [3,2,3]
   Output: 3
   ```

   **Example 2:**

   ```
   Input: [2,2,1,1,1,2,2]
   Output: 2
   ```

   ```c++
   class Solution {
   public:
       int majorityElement(vector<int>& nums) {
           sort(nums.begin(), nums.end());
   //         map<int,int> m;
   //         int majorityInt = nums.size()/2;
   //         for(int i = 0 ; i < nums.size(); i++)
   //         {
   //             if(!m.find(nums[i])->second)
   //                 m.insert(pair<int,int>(nums[i], 1));
   //             else
   //                 m.insert(pair<int,int>(nums[i], (m.find(nums[i])->second)++ ));
               
   //             if(m.find(nums[i])->second > majorityInt)
   //                 return nums[i];
   //         }
   //         std::map<int,int>::iterator it = m.begin();
   //         for (it=m.begin(); it!=m.end(); ++it)
   //             std::cout << it->first << " => " << it->second << '\n';
           
           return nums[nums.size()/2];
           
           return 0;
       }
   };
   ```

10.  **Contains Duplicate** - Easy

    [site](https://leetcode.com/problems/contains-duplicate/)

    Given an array of integers, find if the array contains any duplicates.

    Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

    **Example 1:**

    ```
    Input: [1,2,3,1]
    Output: true
    ```

    **Example 2:**

    ```
    Input: [1,2,3,4]
    Output: false
    ```

    **Example 3:**

    ```
    Input: [1,1,1,3,3,4,3,2,4,2]
    Output: true
    ```

    

    ```c++
    class Solution {
    public:
        bool containsDuplicate(vector<int>& nums) {
            cout << nums.size() ;
            if(nums.size() < 2)
                return 0;
            sort(nums.begin(), nums.end());
    
            for(int i = 0 ; i < nums.size()-1;i++)
                if(nums[i] == nums[i+1])
                    return true;
            
            return false;
        }
    };
    ```

    

11. Kth Largest Element in an Array - Medium

    [site](https://leetcode.com/problems/kth-largest-element-in-an-array/)

    Find the **k**th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

    **Example 1:**

    ```
    Input: [3,2,1,5,6,4] and k = 2
    Output: 5
    ```

    **Example 2:**

    ```
    Input: [3,2,3,1,2,4,5,5,6] and k = 4
    Output: 4
    ```

    **Note:**
    You may assume k is always valid, 1 ≤ k ≤ array's length.

    ```c++
    class Solution {
    public:
        int findKthLargest(vector<int>& nums, int k) {
            sort(nums.begin(), nums.end());
            
            int cnt=1;
            int result = 0;
            for(int i = nums.size()-1; i > 0; i--)
            {
                if(nums[i] != nums[i-1])
                    cnt++;
                if(k == 1 || cnt == k)
                {
                    result = i;
                    break;
                }
            }
            
            return nums[result];
        }
    };
    ```

    

12. Jump Game - Medium

    [site](https://leetcode.com/problems/jump-game/)

    Given an array of non-negative integers, you are initially positioned at the first index of the array.

    Each element in the array represents your maximum jump length at that position.

    Determine if you are able to reach the last index.

    **Example 1:**

    ```
    Input: [2,3,1,1,4]
    Output: true
    Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
    ```

    **Example 2:**

    ```
    Input: [3,2,1,0,4]
    Output: false
    Explanation: You will always arrive at index 3 no matter what. Its maximum
                 jump length is 0, which makes it impossible to reach the last index.
    ```

    ```c++
    #include <algorithm>
    class Solution {
    public:
        bool canJump(vector<int>& nums) {
            if(nums.size() == 0)
                return false;
            int n = nums.size();
            int space = 0;
            for(int i = 0 ; i < n ; i++)
            {
                if(i > space || space  >= n-1)
                    break;
                space = max(space, i+nums[i]);
            }
            return space >= n-1; //O(N);
            // for(int i=1, step=nums[0];i<nums.size();++i){
            //     step--;
            //     if(step < 0)
            //        return false;
            //     if(nums[i] > step)
            //        step = nums[i];
            // }
            // return true;
        }
    };
    ```

13. Find First and Last Position of Element in Sorted Array - Medium

    [site](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

    Given an array of integers `nums` sorted in ascending order, find the starting and ending position of a given `target` value.

    Your algorithm's runtime complexity must be in the order of *O*(log *n*).

    If the target is not found in the array, return `[-1, -1]`.

    **Example 1:**

    ```
    Input: nums = [5,7,7,8,8,10], target = 8
    Output: [3,4]
    ```

    **Example 2:**

    ```
    Input: nums = [5,7,7,8,8,10], target = 6
    Output: [-1,-1]
    ```

    ```c++
    class Solution {
    public:
        vector<int> searchRange(vector<int>& nums, int target) {
            vector<int> result = {-1,-1};
            
            for(int i = 0 ; i < nums.size(); i++)
            {
                if(nums[i] == target)
                {
                    result[0] = i;
                    break;
                }
            }
            
            for(int i = nums.size()-1; i >= 0; i--)
            {
                if(nums[i] == target)
                {
                    result[1] = i;
                    break;
                }
            }
            return result;
        }
    };
    ```

14. Container With Most Water - Medium

    [site](https://leetcode.com/problems/container-with-most-water/)

    Given *n* non-negative integers *a1*, *a2*, ..., *an* , where each represents a point at coordinate (*i*, *ai*). *n* vertical lines are drawn such that the two endpoints of line *i* is at (*i*, *ai*) and (*i*, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

    **Note:** You may not slant the container and *n* is at least 2.

     

    ![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

    The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

     

    **Example:**

    ```
    Input: [1,8,6,2,5,4,8,3,7]
    Output: 49
    ```

    ```c++
    class Solution {
    public:
        int maxArea(vector<int>& height) {
            int contain = 0 , l = 0, r= height.size() -1;
            while(l < r){
                contain = max(contain, min(height[l],height[r])*(r-l));
                if(height[l] < height[r])
                    l++;
                else
                    r--;
            }
            /*
            int contain = 0;
            for(int i = 0 ; i < height.size(); i++){
                for(int j = i+1; j < height.size(); j++){
                    contain = max(contain, min(height[i], height[j])*(j-i));
                }
            }
            */
            return contain;
            
        }
    };
    ```

15. Best Time to Buy and Sell Stock - Easy

    [site](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

    Say you have an array for which the *i*th element is the price of a given stock on day *i*.

    If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

    Note that you cannot sell a stock before you buy one.

    **Example 1:**

    ```
    Input: [7,1,5,3,6,4]
    Output: 5
    Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
                 Not 7-1 = 6, as selling price needs to be larger than buying price.
    ```

    **Example 2:**

    ```
    Input: [7,6,4,3,1]
    Output: 0
    Explanation: In this case, no transaction is done, i.e. max profit = 0.
    ```

    ```c++
    
    ```

16. Best Time to Buy and Sell Stock II - Easy

    [site](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

    Say you have an array for which the *i*th element is the price of a given stock on day *i*.

    Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

    **Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

    **Example 1:**

    ```
    Input: [7,1,5,3,6,4]
    Output: 7
    Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
                 Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
    ```

    **Example 2:**

    ```
    Input: [1,2,3,4,5]
    Output: 4
    Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
                 Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
                 engaging multiple transactions at the same time. You must sell before buying again.
    ```

    **Example 3:**

    ```
    Input: [7,6,4,3,1]
    Output: 0
    Explanation: In this case, no transaction is done, i.e. max profit = 0.
    ```

    ```c++
    class Solution {
    public:
        int maxProfit(vector<int>& prices) {
            if(prices.size() == 0)
                return 0;
            int max = 0;
            for(int i = 1 ; i < prices.size();i++)
            {
                if(prices[i] > prices[i-1])
                {
                    max += prices[i] - prices[i-1];
                }
            }
            return max;
        }
    };
    ```

17. 3Sum - Medium

    [site](https://leetcode.com/problems/3sum/)

    Given an array `nums` of *n* integers, are there elements *a*, *b*, *c* in `nums` such that *a* + *b* + *c* = 0? Find all unique triplets in the array which gives the sum of zero.

    **Note:**

    The solution set must not contain duplicate triplets.

    **Example:**

    ```
    Given array nums = [-1, 0, 1, 2, -1, -4],
    
    A solution set is:
    [
      [-1, 0, 1],
      [-1, -1, 2]
    ]
    ```

    ```c++
    class Solution {
    public:
        vector<vector<int>> threeSum(vector<int>& nums) {
            //two points
            vector<vector<int>> result;
            if(nums.size() < 2)
                return result;
            sort(nums.begin(), nums.end());
            for(int i = 0 ; i < nums.size(); i++){
                if(i > 0 && nums[i] == nums[i-1])
                    continue;
                int l = i+1 , r = nums.size()-1;
                while(l < r){
                    int sum = nums[i] + nums[l] + nums[r];
                    if(sum > 0) r--;
                    else if(sum < 0) l++;
                    else{
                        result.push_back(vector<int> {nums[i] , nums[l] , nums[r]});
                        while(l < nums.size()-2 && nums[l] == nums[l+1] )l++;
                        while(r > 0 && nums[r] == nums[r-1])r--;
                        l++; r--;
                    }
                }
            }
            
            return result;
        }
    };
    
    
    ```

18. 11004 - K번째 수

    [site](https://www.acmicpc.net/problem/11004)

    | 시간 제한 | 메모리 제한 | 제출  | 정답 | 맞은 사람 | 정답 비율 |
    | :-------- | :---------- | :---- | :--- | :-------- | :-------- |
    | 2 초      | 512 MB      | 24700 | 7466 | 4362      | 36.356%   |

    ## 문제

    수 N개 A1, A2, ..., AN이 주어진다. A를 오름차순 정렬했을 때, 앞에서부터 K번째 있는 수를 구하는 프로그램을 작성하시오.

    ## 입력

    첫째 줄에 N(1 ≤ N ≤ 5,000,000)과 K (1 ≤ K ≤ N)이 주어진다.

    둘째에는 A1, A2, ..., AN이 주어진다. (-109 ≤ Ai ≤ 109)

    ## 출력

    A를 정렬했을 때, 앞에서부터 K번째 있는 수를 출력한다.

    ## 예제 입력 1 복사

    ```
    5 2
    4 1 2 3 5
    ```

    ## 예제 출력 1 복사

    ```
    2
    ```

    ```c++
    //
    //  K번째 수(11004).cpp
    //  Algorithm_study
    //
    //  Created by Yeo Kyu Li on 09/04/2019.
    //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
    //
    
    #include <iostream>
    #include <algorithm>
    
    using namespace std;
    
    int main()
    {
        ios::sync_with_stdio(false);
        int cnt, k;
        cin >> cnt >> k;
        
        int* arr = new int[cnt];
        
        for(int i = 0 ; i < cnt ;i ++){
            cin >> arr[i];
        }
        sort(&arr[0], &arr[cnt]);
        
        cout << arr[k-1] << endl;
        delete []arr;
        return 0;
    }
    //#include <iostream>
    //#include <algorithm>
    //#include <vector>
    //
    //using namespace std;
    //
    //int main()
    //{
    //    int cnt, k;
    //    cin >> cnt >> k;
    //
    //    vector<int> v;
    //
    //    for(int i = 0 ; i < cnt; i++){
    //        int num;
    //        cin >> num;
    //        v.push_back(num);
    //    }
    //    sort(v.begin(), v.end());
    //
    //    cout << v[k-1] << endl;
    //
    //    return 0;
    //}
    
    
    ```

19. s

    ```c++
    
    ```

20. s

    ```c++
    
    ```

21. s

    ```c++
    
    ```

22. s

    ```c++
    
    ```

23. s

    ```c++
    
    ```

24. s

    ```c++
    
    ```

25. s

    ```c++
    
    ```

26. s

    ```c++
    
    ```

27. s

    ```c++
    
    ```

    

28. s

    ```c++
    
    ```

29. s

    ```c++
    
    ```

30. s

    ```c++
    
    ```

    

​	