# String

1. String - 문자열 압축

[Original MD](/Users/yeokyuli/Google Drive/KyuLi/구글/Data-Structure/Algorithm Study/20200105.md)

[문제사이트](https://programmers.co.kr/learn/courses/30/lessons/60057)

###### 문제 설명

데이터 처리 전문가가 되고 싶은 **어피치**는 문자열을 압축하는 방법에 대해 공부를 하고 있습니다. 최근에 대량의 데이터 처리를 위한 간단한 비손실 압축 방법에 대해 공부를 하고 있는데, 문자열에서 같은 값이 연속해서 나타나는 것을 그 문자의 개수와 반복되는 값으로 표현하여 더 짧은 문자열로 줄여서 표현하는 알고리즘을 공부하고 있습니다.
간단한 예로 aabbaccc의 경우 2a2ba3c(문자가 반복되지 않아 한번만 나타난 경우 1은 생략함)와 같이 표현할 수 있는데, 이러한 방식은 반복되는 문자가 적은 경우 압축률이 낮다는 단점이 있습니다. 예를 들면, abcabcdede와 같은 문자열은 전혀 압축되지 않습니다. 어피치는 이러한 단점을 해결하기 위해 문자열을 1개 이상의 단위로 잘라서 압축하여 더 짧은 문자열로 표현할 수 있는지 방법을 찾아보려고 합니다.

예를 들어, ababcdcdababcdcd의 경우 문자를 1개 단위로 자르면 전혀 압축되지 않지만, 2개 단위로 잘라서 압축한다면 2ab2cd2ab2cd로 표현할 수 있습니다. 다른 방법으로 8개 단위로 잘라서 압축한다면 2ababcdcd로 표현할 수 있으며, 이때가 가장 짧게 압축하여 표현할 수 있는 방법입니다.

다른 예로, abcabcdede와 같은 경우, 문자를 2개 단위로 잘라서 압축하면 abcabc2de가 되지만, 3개 단위로 자른다면 2abcdede가 되어 3개 단위가 가장 짧은 압축 방법이 됩니다. 이때 3개 단위로 자르고 마지막에 남는 문자열은 그대로 붙여주면 됩니다.

압축할 문자열 s가 매개변수로 주어질 때, 위에 설명한 방법으로 1개 이상 단위로 문자열을 잘라 압축하여 표현한 문자열 중 가장 짧은 것의 길이를 return 하도록 solution 함수를 완성해주세요.

### 제한사항

- s의 길이는 1 이상 1,000 이하입니다.
- s는 알파벳 소문자로만 이루어져 있습니다.

##### 입출력 예

| s                            | result |
| ---------------------------- | ------ |
| `"aabbaccc"`                 | 7      |
| `"ababcdcdababcdcd"`         | 9      |
| `"abcabcdede"`               | 8      |
| `"abcabcabcabcdededededede"` | 14     |
| `"xababcdcdababcdcd"`        | 17     |

```c++
#include <string>
#include <vector>
#include <iostream>
#include <algorithm> 

// 1. 잘라 볼 수 있는 범위는 s.length()/2
// 2. 문자열을 자르는 크기에 맞춰 subStr을 만들어서 비교한다. 문자열 끝까지 가면서 잘라본다, 범위는 자르는 수 만큼 빼고,-> outOfRange.
//     subStr이 똑같으면 cnt++; 
//     cnt > 1 && subStr끼리 안 똑같으면 -> tmp += cnt + subStr
//     cnt == 1 && subStr끼리 안 똑같으면 -> tmp += subStr
// 3. 잘라 볼 수 있는 범위 끝까지 돌려서 answer를 구함 tmp.length()랑 비교해서 answer update.

using namespace std;

int solution(string s) {
    int sLen = s.length();
    int answer = s.length();
    for(int i = 1 ; i <= sLen/2; i++) // 자르는 자리
    {
        string base = "", curStr = "", tmp = "";
        int cnt=1;
        base = s.substr(0,i);
        for(int j = i; j < sLen; j=j+i)
        {
            curStr = s.substr(j,i);
            if(base == curStr)
            {
                cnt++;
                if(j+i >= sLen)
                {
                    if(cnt > 1)
                        tmp += to_string(cnt);
                    tmp+= base;
                }
            }
            else
            {
                if(cnt > 1)
                {
                    tmp += to_string(cnt);
                    cnt = 1;
                }
                tmp += base;
                if(j+i >= sLen)
                    tmp+= curStr;
                base = curStr;
            }
        }

        // cout << tmp << " " << tmp.length() << endl;
        
        if( answer > tmp.length())
            answer = tmp.length();
    }
    
    return answer;
}
```



2. Valid Parentheses - easy

[site](https://leetcode.com/problems/valid-parentheses/)

Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

**Example 1:**

```
Input: "()"
Output: true
```

**Example 2:**

```
Input: "()[]{}"
Output: true
```



```c++
#include <map>
class Solution {
    map<char, char> maps = {
        {')', '('},
        {'}', '{'},
        {']', '['},
    };
public:
    bool isValid(string s) {
        vector<char> st;
        
        if(s.length() == 0)
            return true;
        
        st.push_back(s[0]);
        for(int i = 1 ; i < s.size() ; i++){
            if(!st.empty() && st.back() == maps[s[i]])
                st.pop_back();
            else
                st.push_back(s[i]);
        }
        if(st.empty())
            return true;
        else
            return false;
    }
};
```



3. Two Sum - easy

   [site](https://leetcode.com/problems/two-sum/)

   Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

   You may assume that each input would have ***exactly\*** one solution, and you may not use the *same* element twice.

   **Example:**

   ```
   Given nums = [2, 7, 11, 15], target = 9,
   
   Because nums[0] + nums[1] = 2 + 7 = 9,
   return [0, 1].
   ```

```c++
#include <iostream>
#include <vector>
using namespace std;
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> v;
        for(int i = 0 ; i < nums.size()-1; i++){
            for(int j = 1; j < nums.size(); j++){
                if(i==j)
                    continue;
                else if(nums[i]+nums[j] == target){
                    v.push_back(i);
                    v.push_back(j);
                    return v;
                }
            }
        }
        return v;
    }
};
```



4. string to integer (atoi) - Medium 

[site](https://leetcode.com/problems/string-to-integer-atoi/)

Implement `atoi` which converts a string to an integer.

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned.

**Note:**

- Only the space character `' '` is considered as whitespace character.
- Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231, 231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.

**Example 1:**

```
Input: "42"
Output: 42
```

**Example 2:**

```
Input: "   -42"
Output: -42
Explanation: The first non-whitespace character is '-', which is the minus sign.
             Then take as many numerical digits as possible, which gets 42.
```

**Example 3:**

```
Input: "4193 with words"
Output: 4193
Explanation: Conversion stops at digit '3' as the next character is not a numerical digit.
```

**Example 4:**

```
Input: "words and 987"
Output: 0
Explanation: The first non-whitespace character is 'w', which is not a numerical 
             digit or a +/- sign. Therefore no valid conversion could be performed.
```

**Example 5:**

```
Input: "-91283472332"
Output: -2147483648
Explanation: The number "-91283472332" is out of the range of a 32-bit signed integer.
             Thefore INT_MIN (−231) is returned.
```

```c++
class Solution {
public:
    int myAtoi(string str) {
        int result;
        try{
            result = stoi(str);
        }catch(std::out_of_range& e){
            if(str.find("-") != std::string::npos)
                result = INT_MIN;
            else
                result = INT_MAX;
        }catch(std::invalid_argument& e){
            result = 0;
        }
        return result;
    }
};
```



5. Search in Rotated Sorted Array - Medium

   Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

   (i.e., `[0,1,2,4,5,6,7]` might become `[4,5,6,7,0,1,2]`).

   You are given a target value to search. If found in the array return its index, otherwise return `-1`.

   You may assume no duplicate exists in the array.

   Your algorithm's runtime complexity must be in the order of *O*(log *n*).

   **Example 1:**

   ```
   Input: nums = [4,5,6,7,0,1,2], target = 0
   Output: 4
   ```

   **Example 2:**

   ```
   Input: nums = [4,5,6,7,0,1,2], target = 3
   Output: -1
   ```

   ```c++
   class Solution {
   public:
       int search(vector<int>& nums, int target) {
           int result;
           for(int i = 0 ; i < nums.size(); i++)
           {
               if(nums[i] == target)
                   return i;
           }
           
           return -1;
       }
   };
   ```

6. Reverse String - Easy

   [site](https://leetcode.com/problems/reverse-string/)

   Write a function that reverses a string. The input string is given as an array of characters `char[]`.

   Do not allocate extra space for another array, you must do this by **modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** with O(1) extra memory.

   You may assume all the characters consist of [printable ascii characters](https://en.wikipedia.org/wiki/ASCII#Printable_characters).

    

   **Example 1:**

   ```
   Input: ["h","e","l","l","o"]
   Output: ["o","l","l","e","h"]
   ```

   **Example 2:**

   ```
   Input: ["H","a","n","n","a","h"]
   Output: ["h","a","n","n","a","H"]
   ```

   ```c++
   class Solution {
   public:
       void reverseString(vector<char>& s) {
           
           int r = s.size()-1;
           int l = 0;
           
           while(l < r)
           {
               if(s[l] != s[r])
               {
                   char ch = s[l];
                   s[l] = s[r];
                   s[r] = ch;
               }
               l++;
               r--;
           }
           
       }
   };
   ```

7. Reverse Integer - Easy

   [site](https://leetcode.com/problems/reverse-integer/)

   Given a 32-bit signed integer, reverse digits of an integer.

   **Example 1:**

   ```
   Input: 123
   Output: 321
   ```

   **Example 2:**

   ```
   Input: -123
   Output: -321
   ```

   **Example 3:**

   ```
   Input: 120
   Output: 21
   ```

   **Note:**
   Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231, 231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

   ```c++
   #include <deque>
   #include <string>
   #include <cstdlib>
   #include <limits> 
   using namespace std;
   class Solution {
   public:
       /*
        int reverse(int x) {
           long long int lx = x;
           long long int ret = 0;
           while (lx != 0)
           {
               ret = ret * 10 + lx % 10;
               lx /= 10;
           }
           if (ret > INT_MAX || ret < INT_MIN) return 0;
           return (int)ret;
       }
       */
       int reverse(int x) {
           //if(x > std::numeric_limits<int>::max() || x < std::numeric_limits<int>::min()) return 0;
           if(x > INT_MAX || x < INT_MIN) return 0;
           string str = to_string(x);
           deque <int> que;
           string result="";
           for(int i = str.size()-1; i >=0 ; i--){
               if(str[i] == '-')
                   que.push_front(str[i]);
               else if(i == str.size()-1 && str[i]==0)
                   break;
               else
                   que.push_back(str[i]);
           }
           while(!que.empty()){
               result += (que.front());
               que.pop_front();
           }
           try{
               stoi(result);
           }catch(std::out_of_range& e){
               return 0;
           }
   
           return stoi(result);
       }
   };
   ```

8. Remove Element - Esay

   [site](https://leetcode.com/problems/remove-element/)

   Given an array *nums* and a value *val*, remove all instances of that value [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) and return the new length.

   Do not allocate extra space for another array, you must do this by **modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** with O(1) extra memory.

   The order of elements can be changed. It doesn't matter what you leave beyond the new length.

   **Example 1:**

   ```
   Given nums = [3,2,2,3], val = 3,
   
   Your function should return length = 2, with the first two elements of nums being 2.
   
   It doesn't matter what you leave beyond the returned length.
   ```

   **Example 2:**

   ```
   Given nums = [0,1,2,2,3,0,4,2], val = 2,
   
   Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.
   
   Note that the order of those five elements can be arbitrary.
   
   It doesn't matter what values are set beyond the returned length.
   ```

   **Clarification:**

   Confused why the returned value is an integer but your answer is an array?

   Note that the input array is passed in by **reference**, which means modification to the input array will be known to the caller as well.

   Internally you can think of this:

   ```
   // nums is passed in by reference. (i.e., without making a copy)
   int len = removeElement(nums, val);
   
   // any modification to nums in your function would be known by the caller.
   // using the length returned by your function, it prints the first len elements.
   for (int i = 0; i < len; i++) {
       print(nums[i]);
   }
   ```

   ```c++
   class Solution {
   public:
       int removeElement(vector<int>& nums, int val) {
           int i = 0;        
           int length = nums.size();
           cout << length << endl;
           while(i < length)
           {
               if(nums[i] == val)
               {
                   nums[i] = nums[length-1];
                   length--;
               }
               else
                   i++;
               
           }
           
           return length;
       }
   };
   ```

9.  Longest Common Prefix - Easy

   [site](https://leetcode.com/problems/longest-common-prefix/)

   Write a function to find the longest common prefix string amongst an array of strings.

   If there is no common prefix, return an empty string `""`.

   **Example 1:**

   ```
   Input: ["flower","flow","flight"]
   Output: "fl"
   ```

   **Example 2:**

   ```
   Input: ["dog","racecar","car"]
   Output: ""
   Explanation: There is no common prefix among the input strings.
   ```

   **Note:**

   All given inputs are in lowercase letters `a-z`.

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

10. Implement strStr() - Easy

    Implement [strStr()](http://www.cplusplus.com/reference/cstring/strstr/).

    Return the index of the first occurrence of needle in haystack, or **-1** if needle is not part of haystack.

    **Example 1:**

    ```
    Input: haystack = "hello", needle = "ll"
    Output: 2
    ```

    **Example 2:**

    ```
    Input: haystack = "aaaaa", needle = "bba"
    Output: -1
    ```

    **Clarification:**

    What should we return when `needle` is an empty string? This is a great question to ask during an interview.

    For the purpose of this problem, we will return 0 when `needle` is an empty string. This is consistent to C's [strstr()](http://www.cplusplus.com/reference/cstring/strstr/) and Java's [indexOf()](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)).

    ```c++
    #include <string>
    class Solution {
    public:
        int strStr(string haystack, string needle) {
            int result = -1;
            int length = needle.size();
            
            if(haystack.size() < needle.size())
                return result;
            
            for(int i = 0 ; i < haystack.size() - length +1 ; i++)
            {
                if(haystack.substr(i, length)  == needle)
                {
                    result = i;
                    break;
                }
            }
            
            return result;
        }
    };
    ```

11. Count and Say - Easy

    [site](https://leetcode.com/problems/count-and-say/)

    The count-and-say sequence is the sequence of integers with the first five terms as following:

    ```
    1.     1
    2.     11
    3.     21
    4.     1211
    5.     111221
    ```

    `1` is read off as `"one 1"` or `11`.
    `11` is read off as `"two 1s"` or `21`.
    `21` is read off as `"one 2`, then `one 1"` or `1211`.

    Given an integer *n* where 1 ≤ *n* ≤ 30, generate the *n*th term of the count-and-say sequence. You can do so recursively, in other words from the previous member read off the digits, counting the number of digits in groups of the same digit.

    Note: Each term of the sequence of integers will be represented as a string.

     

    **Example 1:**

    ```
    Input: 1
    Output: "1"
    Explanation: This is the base case.
    ```

    **Example 2:**

    ```
    Input: 4
    Output: "1211"
    Explanation: For n = 3 the term was "21" in which we have two groups "2" and "1", "2" can be read as "12" which means frequency = 1 and value = 2, the same way "1" is read as "11", so the answer is the concatenation of "12" and "11" which is "1211".
    ```

    ```c++
    #include <map>
    class Solution {
    public:
        // map<int, string> maps = 
        // {
        //     {1, "1"},
        //     {2, "11"},
        //     {3, "21"},
        //     {4, "1211"},
        //     {5, "111221"}
        // };
        string countAndSay(int n) {
            map<int, string> maps;
            for(int i = 1; i <=n; i++)
            {
                if(i==1)
                    maps.insert(make_pair(1, "1"));
                else
                {
                    string pre = maps.find(i-1)->second;
                    cout << "pre = " << pre << endl;
                    string tmp = "";
                    int cnt = 1;
                    for(int j = 0; j < pre.size() ; j++)
                    {
                        if(pre[j] != pre[j+1])
                        {
                            tmp = tmp + to_string(cnt) + pre[j];
                            cnt = 1;
                        }
                        else
                            cnt++;
                        
                    }
                    maps.insert(make_pair(i, tmp));
                }
            }
            return maps.find(n)->second;
        }
    };
    ```

12. Longest Substring Without Repeating Characters - Medium

    [site](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

    Given a string, find the length of the **longest substring** without repeating characters.

    **Example 1:**

    ```
    Input: "abcabcbb"
    Output: 3 
    Explanation: The answer is "abc", with the length of 3. 
    ```

    **Example 2:**

    ```
    Input: "bbbbb"
    Output: 1
    Explanation: The answer is "b", with the length of 1.
    ```

    **Example 3:**

    ```
    Input: "pwwkew"
    Output: 3
    Explanation: The answer is "wke", with the length of 3. 
                 Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
    ```

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

13. Longest Palindromic Substring - Medium

    [site](https://leetcode.com/problems/longest-palindromic-substring/)

    Given a string **s**, find the longest palindromic substring in **s**. You may assume that the maximum length of **s** is 1000.

    **Example 1:**

    ```
    Input: "babad"
    Output: "bab"
    Note: "aba" is also a valid answer.
    ```

    **Example 2:**

    ```
    Input: "cbbd"
    Output: "bb"
    ```

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
                if(i<=r) R[i] = min(r-i, R[2*k-i]);
                
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

14. Generate Parentheses - Medium

    [site](https://leetcode.com/problems/generate-parentheses/)

    Given *n* pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

    For example, given *n* = 3, a solution set is:

    ```
    [
      "((()))",
      "(()())",
      "(())()",
      "()(())",
      "()()()"
    ]
    ```

    ```c++
    class Solution {
    public:
        vector<string> result;
        
        void generate(string str, int left, int right, int size)
        {
            if(str.length() == size*2)
                result.push_back(str);
            
            if(left < size)
                generate(str+"(", left+1, right, size);
            if(right < left)
                generate(str+")", left, right+1, size); 
            
            
        }
        
        vector<string> generateParenthesis(int n) {
            int right = 0, left = 0, size = n;
            generate("", left, right, size);        
            
            return result;
        }
    };
    ```

15. 괄호 9012

    [site](https://www.acmicpc.net/problem/9012) 

    | 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
    | :-------- | :---------- | :---- | :---- | :-------- | :-------- |
    | 1 초      | 128 MB      | 51237 | 20453 | 14821     | 39.018%   |

    ## 문제

    괄호 문자열(Parenthesis String, PS)은 두 개의 괄호 기호인 ‘(’ 와 ‘)’ 만으로 구성되어 있는 문자열이다. 그 중에서 괄호의 모양이 바르게 구성된 문자열을 올바른 괄호 문자열(Valid PS, VPS)이라고 부른다. 한 쌍의 괄호 기호로 된 “( )” 문자열은 기본 VPS 이라고 부른다. 만일 x 가 VPS 라면 이것을 하나의 괄호에 넣은 새로운 문자열 “(x)”도 VPS 가 된다. 그리고 두 VPS x 와 y를 접합(concatenation)시킨 새로운 문자열 xy도 VPS 가 된다. 예를 들어 “(())()”와 “((()))” 는 VPS 이지만 “(()(”, “(())()))” , 그리고 “(()” 는 모두 VPS 가 아닌 문자열이다. 

    여러분은 입력으로 주어진 괄호 문자열이 VPS 인지 아닌지를 판단해서 그 결과를 YES 와 NO 로 나타내어야 한다. 

    ## 입력

    입력 데이터는 표준 입력을 사용한다. 입력은 T개의 테스트 데이터로 주어진다. 입력의 첫 번째 줄에는 입력 데이터의 수를 나타내는 정수 T가 주어진다. 각 테스트 데이터의 첫째 줄에는 괄호 문자열이 한 줄에 주어진다. 하나의 괄호 문자열의 길이는 2 이상 50 이하이다. 

    ## 출력

    출력은 표준 출력을 사용한다. 만일 입력 괄호 문자열이 올바른 괄호 문자열(VPS)이면 “YES”, 아니면 “NO”를 한 줄에 하나씩 차례대로 출력해야 한다. 

    ## 예제 입력 1 복사

    ```
    6
    (())())
    (((()())()
    (()())((()))
    ((()()(()))(((())))()
    ()()()()(()()())()
    (()((())()(
    ```

    ## 예제 출력 1 복사

    ```
    NO
    NO
    YES
    NO
    YES
    NO
    ```

    ```c++
    //
    //  괄호(9012).cpp
    //  Algorithm_study
    //
    //  Created by Yeo Kyu Li on 26/03/2019.
    //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
    //
    
    #include <iostream>
    #include <stack>
    #include <string>
    using namespace std;
    int main()
    {
        ios_base::sync_with_stdio(0);
        cin.tie(0); //cin 실행속도 향상
        int cnt;
        string str;
        cin >> cnt;
        
        while(cnt--){
            stack<int> st;
            bool wrong = false;
            cin >> str;
            
            for(auto c:str){
                if(c == '('){
                    st.push(c);
                }
                else if(c== ')'){
                    if(st.empty()){
                        wrong = true;
                        break;
                    }
                    else{
                        st.pop();
                    }
                }
            }
            if (st.empty() && !wrong)
            {
                cout << "YES" << endl;
            }
            else{
                cout << "NO" << endl;
            }
        }
        return 0;
    }
    
    ```

16. 10799 쇠막대기

    [site](https://www.acmicpc.net/problem/10799)

    | 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
    | :-------- | :---------- | :---- | :---- | :-------- | :-------- |
    | 1 초      | 256 MB      | 16639 | 10020 | 7234      | 60.724%   |

    ## 문제

    여러 개의 쇠막대기를 레이저로 절단하려고 한다. 효율적인 작업을 위해서 쇠막대기를 아래에서 위로 겹쳐 놓고, 레이저를 위에서 수직으로 발사하여 쇠막대기들을 자른다. 쇠막대기와 레이저의 배치는 다음 조건을 만족한다.

    - 쇠막대기는 자신보다 긴 쇠막대기 위에만 놓일 수 있다. - 쇠막대기를 다른 쇠막대기 위에 놓는 경우 완전히 포함되도록 놓되, 끝점은 겹치지 않도록 놓는다.
    - 각 쇠막대기를 자르는 레이저는 적어도 하나 존재한다.
    - 레이저는 어떤 쇠막대기의 양 끝점과도 겹치지 않는다. 

    아래 그림은 위 조건을 만족하는 예를 보여준다. 수평으로 그려진 굵은 실선은 쇠막대기이고, 점은 레이저의 위치, 수직으로 그려진 점선 화살표는 레이저의 발사 방향이다.

    ![img](https://onlinejudgeimages.s3-ap-northeast-1.amazonaws.com/problem/10799/1.png)

    이러한 레이저와 쇠막대기의 배치는 다음과 같이 괄호를 이용하여 왼쪽부터 순서대로 표현할 수 있다.

    1. 레이저는 여는 괄호와 닫는 괄호의 인접한 쌍 ‘( ) ’ 으로 표현된다. 또한, 모든 ‘( ) ’는 반드시 레이저를 표현한다.
    2. 쇠막대기의 왼쪽 끝은 여는 괄호 ‘ ( ’ 로, 오른쪽 끝은 닫힌 괄호 ‘) ’ 로 표현된다. 

    위 예의 괄호 표현은 그림 위에 주어져 있다.

    쇠막대기는 레이저에 의해 몇 개의 조각으로 잘려지는데, 위 예에서 가장 위에 있는 두 개의 쇠막대기는 각각 3개와 2개의 조각으로 잘려지고, 이와 같은 방식으로 주어진 쇠막대기들은 총 17개의 조각으로 잘려진다. 

    쇠막대기와 레이저의 배치를 나타내는 괄호 표현이 주어졌을 때, 잘려진 쇠막대기 조각의 총 개수를 구하는 프로그램을 작성하시오.

    ## 입력

    한 줄에 쇠막대기와 레이저의 배치를 나타내는 괄호 표현이 공백없이 주어진다. 괄호 문자의 개수는 최대 100,000이다. 

    ## 출력

    잘려진 조각의 총 개수를 나타내는 정수를 한 줄에 출력한다.

    ## 예제 입력 1 복사

    ```
    ()(((()())(())()))(())
    ```

    ## 예제 출력 1 복사

    ```
    17
    ```

    ## 예제 입력 2 복사

    ```
    (((()(()()))(())()))(()())
    ```

    ## 예제 출력 2 복사

    ```
    24
    ```

    ```c++
    #include <iostream>
    #include <stack>
    using namespace std;
    int main(){
        stack<int> st;
        string str;
        int result = 0;
    
        getline(cin, str, '\n');
        
        for(int i = 0 ; i < str.length(); i++){
            if (str[i] == '(')
                st.push('(');
            else if(str[i] == ')'){
                st.pop();
                if(str[i-1] == '(')
                    result += st.size();
                else
                    result += 1;
            }
        }
        cout << result << endl;
        
        return 0;
    }
    ```

17. 10808 - 알파벳 개수

    [site](https://www.acmicpc.net/problem/10808)

    | 시간 제한 | 메모리 제한 | 제출  | 정답 | 맞은 사람 | 정답 비율 |
    | :-------- | :---------- | :---- | :--- | :-------- | :-------- |
    | 1 초      | 256 MB      | 12225 | 8251 | 6865      | 68.520%   |

    ## 문제

    알파벳 소문자로만 이루어진 단어 S가 주어진다. 각 알파벳이 단어에 몇 개가 포함되어 있는지 구하는 프로그램을 작성하시오.

    ## 입력

    첫째 줄에 단어 S가 주어진다. 단어의 길이는 100을 넘지 않으며, 알파벳 소문자로만 이루어져 있다.

    ## 출력

    단어에 포함되어 있는 a의 개수, b의 개수, …, z의 개수를 공백으로 구분해서 출력한다.

    ## 예제 입력 1 복사

    ```
    baekjoon
    ```

    ## 예제 출력 1 복사

    ```
    1 1 0 0 1 0 0 0 0 1 1 0 0 1 2 0 0 0 0 0 0 0 0 0 0 0
    ```

    ```c++
    //
    //  알파벳 개수(10808).cpp
    //  Algorithm_study
    //
    //  Created by Yeo Kyu Li on 29/03/2019.
    //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
    //
    #include <iostream>
    #include <algorithm>
    #include <string>
    using namespace std;
    // a - 97 == 0
    int alphabet[26];
    int main()
    {
        string str;
        cin >> str;
        for(int i = 0 ; i <str.length() ; i++){
            alphabet[str[i]-'a']++;
        }
        for(int j = 0 ; j < 26 ; j++)
            cout << alphabet[j] << " ";
        cout << endl;
        
    //    for(char a = 'a' ; a <= 'z'; a++){
    //        cout<< count(str.begin(), str.end(), a) << " ";
    //    }
    //    cout << endl;
        return 0;
    }
    
    ```

18. 10809 - 알파벳 찾기

    [site](https://www.acmicpc.net/problem/10809)

    | 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
    | :-------- | :---------- | :---- | :---- | :-------- | :-------- |
    | 1 초      | 256 MB      | 38851 | 21207 | 18100     | 55.797%   |

    ## 문제

    알파벳 소문자로만 이루어진 단어 S가 주어진다. 각각의 알파벳에 대해서, 단어에 포함되어 있는 경우에는 처음 등장하는 위치를, 포함되어 있지 않은 경우에는 -1을 출력하는 프로그램을 작성하시오.

    ## 입력

    첫째 줄에 단어 S가 주어진다. 단어의 길이는 100을 넘지 않으며, 알파벳 소문자로만 이루어져 있다.

    ## 출력

    각각의 알파벳에 대해서, a가 처음 등장하는 위치, b가 처음 등장하는 위치, ... z가 처음 등장하는 위치를 공백으로 구분해서 출력한다.

    만약, 어떤 알파벳이 단어에 포함되어 있지 않다면 -1을 출력한다. 단어의 첫 번째 글자는 0번째 위치이고, 두 번째 글자는 1번째 위치이다.

    ## 예제 입력 1 복사

    ```
    baekjoon
    ```

    ## 예제 출력 1 복사

    ```
    1 0 -1 -1 2 -1 -1 -1 -1 4 3 -1 -1 7 5 -1 -1 -1 -1 -1 -1 -1 -1 -1 -1 -1
    ```

    ```c++
    //
    //  알파벳 찾기(10809).cpp
    //  Algorithm_study
    //
    //  Created by Yeo Kyu Li on 29/03/2019.
    //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
    //
    #include <iostream>
    #include <string>
    using namespace std;
    int main(){
        int alphabet[26];
        fill_n(alphabet, 26, -1);
        string str;
        
        cin >> str;
        
        for(int i = 0 ; i < str.length(); i++){
            if((alphabet[str[i] - 'a']) == -1)
                alphabet[str[i] - 'a'] = i;
        }
    
        for(int j = 0 ; j < 26; j++)
            cout << alphabet[j] << " ";
        cout << endl;
        
    }
    
    ```

19. 10820 - 문자열 분석

    [site](https://www.acmicpc.net/problem/10820)

    | 시간 제한 | 메모리 제한 | 제출  | 정답 | 맞은 사람 | 정답 비율 |
    | :-------- | :---------- | :---- | :--- | :-------- | :-------- |
    | 1 초      | 256 MB      | 10250 | 4241 | 3512      | 43.145%   |

    ## 문제

    문자열 N개가 주어진다. 이때, 문자열에 포함되어 있는 소문자, 대문자, 숫자, 공백의 개수를 구하는 프로그램을 작성하시오.

    각 문자열은 알파벳 소문자, 대문자, 숫자, 공백으로만 이루어져 있다.

    ## 입력

    첫째 줄부터 N번째 줄까지 문자열이 주어진다. (1 ≤ N ≤ 100) 문자열의 길이는 100을 넘지 않는다.

    ## 출력

    첫째 줄부터 N번째 줄까지 각각의 문자열에 대해서 소문자, 대문자, 숫자, 공백의 개수를 공백으로 구분해 출력한다.

    ## 예제 입력 1 복사

    ```
    This is String
    SPACE    1    SPACE
     S a M p L e I n P u T     
    0L1A2S3T4L5I6N7E8
    ```

    ## 예제 출력 1 복사

    ```
    10 2 0 2
    0 10 1 8
    5 6 0 16
    0 8 9 0
    ```

    ```c++
    //
    //  문자열 분석(10820).cpp
    //  Algorithm_study
    //
    //  Created by Yeo Kyu Li on 29/03/2019.
    //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
    //
    #include <iostream>
    #include <string>
    using namespace std;
    
    int main(){
       
    //    cout << str << endl;
    //    for(char a ='a' ; a <= 'z' ;a++ )
    //        small += count(str.begin(), str.end(), a);
    //    for(char a ='A' ; a <= 'Z' ;a++ )
    //        capital += count(str.begin(), str.end(), a);
    //
    //    for(char a ='1' ; a <= '9' ;a++ )
    //        num += count(str.begin(), str.end(), a);
        string str;
        while(getline(cin, str)){
            int small=0, capital=0, num=0, space=0;
            for(int i = 0 ; i < str.length(); i++){
                if(str[i] >= 'a' and str[i] <= 'z')
                    small++;
                else if(str[i] >= 'A' and str[i] <= 'Z')
                    capital++;
                else if(str[i] >= '0' and str[i] <= '9')
                    num++;
                else if(str[i] == ' ')
                    space++;
            }
            cout << small << " " << capital << " " << num << " " << space << endl;
        }
        return 0;
    }
    
    ```

20. 11655 - ROT13

    [site](https://www.acmicpc.net/problem/11655)

    | 시간 제한 | 메모리 제한 | 제출 | 정답 | 맞은 사람 | 정답 비율 |
    | :-------- | :---------- | :--- | :--- | :-------- | :-------- |
    | 1 초      | 256 MB      | 6918 | 4097 | 3578      | 61.079%   |

    ## 문제

    ROT13은 카이사르 암호의 일종으로 영어 알파벳을 13글자씩 밀어서 만든다.

    예를 들어, "Baekjoon Online Judge"를 ROT13으로 암호화하면 "Onrxwbba Bayvar Whqtr"가 된다. ROT13으로 암호화한 내용을 원래 내용으로 바꾸려면 암호화한 문자열을 다시 ROT13하면 된다. 앞에서 암호화한 문자열 "Onrxwbba Bayvar Whqtr"에 다시 ROT13을 적용하면 "Baekjoon Online Judge"가 된다.

    ROT13은 알파벳 대문자와 소문자에만 적용할 수 있다. 알파벳이 아닌 글자는 원래 글자 그대로 남아 있어야 한다. 예를 들어, "One is 1"을 ROT13으로 암호화하면 "Bar vf 1"이 된다.

    문자열이 주어졌을 때, "ROT13"으로 암호화한 다음 출력하는 프로그램을 작성하시오.

    ## 입력

    첫째 줄에 알파벳 대문자, 소문자, 공백, 숫자로만 이루어진 문자열 S가 주어진다. S의 길이는 100을 넘지 않는다.

    ## 출력

    첫째 줄에 S를 ROT13으로 암호화한 내용을 출력한다.

    ## 예제 입력 1 복사

    ```
    Baekjoon Online Judge
    ```

    ## 예제 출력 1 복사

    ```
    Onrxwbba Bayvar Whqtr
    ```

    ## 예제 입력 2 복사

    ```
    One is 1
    ```

    ## 예제 출력 2 복사

    ```
    Bar vf 1
    ```

    ```c++
    //
    //  ROT13(11655).cpp
    //  Algorithm_study
    //
    //  Created by Yeo Kyu Li on 29/03/2019.
    //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
    //
    #include <iostream>
    
    using namespace std;
    
    int main()
    {
        string str;
        
        getline(cin, str);
        
        for(int i = 0 ; i < str.length() ; i++){
            if(str[i] >= 'A' and str[i] <= 'Z')
                str[i] = (str[i] -'A' + 13)%26 +'A';
            if(str[i] >= 'a' and str[i] <= 'z')
                str[i] = (str[i] -'a' + 13)%26 +'a';
    //        if(str[i] >= 'a' and str[i] <= 'm'){
    //            str[i] += 13;
    //        }
    //        else if(str[i] >= 'n' and str[i] <= 'z'){
    //            str[i] -= 13;
    //        }
    //        if(str[i] >= 'A' and str[i] <= 'M'){
    //            str[i] += 13;
    //        }
    //        else if(str[i] >= 'N' and str[i] <= 'z'){
    //            str[i] -= 13;
    //        }
        }
        cout << str << endl;
        
        return 0;
    }
    
    ```

21. 11719 - 그대로 출력하기 2

    [site](https://www.acmicpc.net/problem/11719)

    | 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
    | :-------- | :---------- | :---- | :---- | :-------- | :-------- |
    | 1 초      | 256 MB      | 45181 | 23367 | 20507     | 57.180%   |

    ## 문제

    입력 받은 대로 출력하는 프로그램을 작성하시오.

    ## 입력

    입력이 주어진다. 입력은 최대 100줄로 이루어져 있고, 알파벳 소문자, 대문자, 공백, 숫자로만 이루어져 있다. 각 줄은 100글자를 넘지 않으며, 빈 줄이 주어질 수도 있고, 각 줄의 앞 뒤에 공백이 있을 수도 있다.

    ## 출력

    입력받은 그대로 출력한다.

    ## 예제 입력 1 복사

    ```
        Hello
    
    Baekjoon     
       Online Judge    
    ```

    ## 예제 출력 1 복사

    ```
        Hello
    
    Baekjoon     
       Online Judge    
    ```

    ```c++
    #include <iostream>
    #include <string>
    using namespace std;
    int main()
    {
        string str;
        for(int i = 0 ; i < 100; i++){
            getline(cin, str);
            cout << str<< endl;
        }
        return 0;
    }
    ```

22. Easy

    ```c++
    
    ```

23. Easy

    ```c++
    
    ```

24. Easy

    ```c++
    
    ```

25. Easy

    ```c++
    
    ```

26. Easy

    ```c++
    
    ```

27. Easy

    ```c++
    
    ```

28. Easy

    ```c++
    
    ```

29. Easy

    ```c++
    
    ```

30. Easy

    ```c++
    
    ```

    