# Hash



1. Top K Frequent Elements

   [site](https://leetcode.com/problems/top-k-frequent-elements/)

   Given a non-empty array of integers, return the ***k\*** most frequent elements.

   **Example 1:**

   ```
   Input: nums = [1,1,1,2,2,3], k = 2
   Output: [1,2]
   ```

   **Example 2:**

   ```
   Input: nums = [1], k = 1
   Output: [1]
   ```

   **Note:**

   - You may assume *k* is always valid, 1 ≤ *k* ≤ number of unique elements.

   - Your algorithm's time complexity **must be** better than O(*n* log *n*), where *n* is the array's size.

     

```c++
class Solution {
public:
    
    struct cmp
    {
        template <typename T>
        bool operator()(const T& l, const T& r) const
        {
            if (l.second != r.second)
                return l.second > r.second;
            return l.first < r.first;
            
        }
    };
    vector<int> topKFrequent(vector<int>& nums, int k) {
        map<int, int> maps;
        vector<int> result;
        for(int i = 0; i < nums.size(); i++)
        {
            if(maps.find(nums[i]) != maps.end())
                maps.find(nums[i])->second++;
            else
                maps.insert(pair<int,int>(nums[i], 1));
        }
        
        set<pair<int,int>, cmp> set(maps.begin(), maps.end());
//         for(auto i = maps.begin() ; i != maps.end(); i++)
//         {
//             cout << maps->first << " " << maps->second;
//         }
        
        
        for(auto a : maps)
        {
            if(k==0)
                return result;
            result.push_back(a.first);
            k--;
        }
        return result;
    }

};
```



2. Single number - Esay

   [site](https://leetcode.com/problems/single-number/)

   Given a **non-empty** array of integers, every element appears *twice* except for one. Find that single one.

   **Note:**

   Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

   **Example 1:**

   ```
   Input: [2,2,1]
   Output: 1
   ```

   **Example 2:**

   ```
   Input: [4,1,2,1,2]
   Output: 4
   ```

   ```c++
   class Solution {
   public:
       int singleNumber(vector<int>& nums) {
           sort(nums.begin(), nums.end());
           
           int cnt = 1;
           int result = 0;
           for(int i= 0; i< nums.size()-1;i++)
           {
               if(nums[i] != nums[i+1])
               {
                   if(cnt == 1)
                   {
                       result = i;
                       break;
                   }
                   result = i+1;
                   cnt=1;
               }
               else
                   cnt++;
           }
           
           return nums[result];
           
       }
   };
   ```

3. First Unique Character in a String 

   [site](https://leetcode.com/problems/first-unique-character-in-a-string/)

   Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

   **Examples:**

   ```
   s = "leetcode"
   return 0.
   
   s = "loveleetcode",
   return 2.
   ```

   

   **Note:** You may assume the string contain only lowercase letters.

   ```c++
   class Solution {
   public:
       //순서대로 map<char, int> 에 넣어줘서 작은 값은 return해주면 index가 나오겠찌?
       int firstUniqChar(string s) {
           map<char, int> maps;
           
           for(int i = 0 ; i < s.size(); i++)
           {
               if(maps.find(s[i]) != maps.end())
                   maps.find(s[i])->second++;
               else
                   maps.insert(pair<char, int>(s[i], 1));
           }
           
           for(int i = 0 ; i < s.size(); i++)
           {
               if(maps.at(s[i]) == 1)
                   return i;
           }
           
           return -1;
       }
   };
   ```

4. Count Primes - Easy

   [site](https://leetcode.com/problems/count-primes/)

   Count the number of prime numbers less than a non-negative number, ***n\***.

   **Example:**

   ```
   Input: 10
   Output: 4
   Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
   ```

   ```c++
   class Solution {
   public:
       int countPrimes(int n) {
           if(n == 0)
               return 0;
           vector<int> v(n+1);
           
           v[0] = 0;
           v[1] = 0;
           for(int i = 2; i < v.size(); i++)
               v[i] = i;
           v[n] = 0;
           for(int i = 2; i < v.size(); i++)
               countPrimes(v, i, n);
   
           return count_if(v.begin(), v.end(),
                               [](int elem) { return elem > 0; });
       }
   
   private:
       void countPrimes(vector<int>& v, int start, int n) {
           
           for(int i = start ; i < v.size(); i = i + start)
           {
               if(v[start] == 0)
                   break;
               
               if(i != start && v[i] != 0)
                   v[i] = 0;
           }
       }
   };
   ```

5. Group Anagrams - Medium

   [site](https://leetcode.com/problems/group-anagrams/)

   Given an array of strings, group anagrams together.

   **Example:**

   ```
   Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
   Output:
   [
     ["ate","eat","tea"],
     ["nat","tan"],
     ["bat"]
   ]
   ```

   **Note:**

   - All inputs will be in lowercase.
   - The order of your output does not matter.

   ```c++
   class Solution {
   public:
       vector<vector<string>> groupAnagrams(vector<string>& strs) {
           unordered_map<string, vector<string>> map;
           
           for(string s : strs){
               string t = s;
               sort(t.begin(), t.end());
               map[t].push_back(s);
           }
           
           vector<vector<string>> result;
           for(auto p : map)
               result.push_back(p.second);
   
           return result;
       }
   };
   ```

6. 5052 전화번호 목록

   [site](https://www.acmicpc.net/problem/5052)

   | 시간 제한 | 메모리 제한 | 제출  | 정답 | 맞은 사람 | 정답 비율 |
   | :-------- | :---------- | :---- | :--- | :-------- | :-------- |
   | 1 초      | 256 MB      | 11644 | 3678 | 2043      | 30.075%   |

   ## 문제

   전화번호 목록이 주어진다. 이때, 이 목록이 일관성이 있는지 없는지를 구하는 프로그램을 작성하시오.

   전화번호 목록이 일관성을 유지하려면, 한 번호가 다른 번호의 접두어인 경우가 없어야 한다.

   예를 들어, 전화번호 목록이 아래와 같은 경우를 생각해보자

   - 긴급전화: 911
   - 상근: 97 625 999
   - 선영: 91 12 54 26

   이 경우에 선영이에게 전화를 걸 수 있는 방법이 없다. 전화기를 들고 선영이 번호의 처음 세 자리를 누르는 순간 바로 긴급전화가 걸리기 때문이다. 따라서, 이 목록은 일관성이 없는 목록이다. 

   ## 입력

   첫째 줄에 테스트 케이스의 개수 t가 주어진다. (1 ≤ t ≤ 50) 각 테스트 케이스의 첫째 줄에는 전화번호의 수 n이 주어진다. (1 ≤ n ≤ 10000) 다음 n개의 줄에는 목록에 포함되어 있는 전화번호가 하나씩 주어진다. 전화번호의 길이는 길어야 10자리이며, 목록에 있는 두 전화번호가 같은 경우는 없다.

   ## 출력

   각 테스트 케이스에 대해서, 일관성 있는 목록인 경우에는 YES, 아닌 경우에는 NO를 출력한다.

   ## 예제 입력 1 복사

   ```
   2
   3
   911
   97625999
   91125426
   5
   113
   12340
   123440
   12345
   98346
   ```

   ## 예제 출력 1 복사

   ```
   NO
   YES
   ```

   ```c++
   //
   //  전화번호 목록 (5052).cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 06/05/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   
   #include <iostream>
   #include <vector>
   #include <algorithm> // sort
   using namespace std;
   
   int main()
   {
       cin.tie(0);
       cout.tie(0);
       ios::sync_with_stdio(false);
       
       int T;
       cin >> T;
       
       while(T--){
           int N;
           cin >> N;
           vector<string> arr(N);
           
           for(int i = 0 ; i < N ; i++){
               cin >> arr[i];
           }
           sort(arr.begin(), arr.end());
   //        sort(arr, arr+N);
           
           bool isConsistency=true;
           for(int i = 1 ; i < arr.size(); i++){
               if(arr[i-1] == arr[i].substr(0, arr[i-1].size())){
                   isConsistency = false;
                   break;
               }
           }
           puts(isConsistency ? "YES" : "NO");
   //        if(isConsistency)
   //            cout << "YES";
   //        else
   //            cout << "NO";
       }
       return 0;
   }
   ```

7. Easy

   ```c++
   
   ```

   