# Bit Manipulation



1.  Divide Two Integers

   Given two integers `dividend` and `divisor`, divide two integers without using multiplication, division and mod operator.

   Return the quotient after dividing `dividend` by `divisor`.

   The integer division should truncate toward zero.

   

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
   
   int stringToInteger(string input) {
       return stoi(input);
   }
   
   int main() {
       string line;
       while (getline(cin, line)) {
           int dividend = stringToInteger(line);
           getline(cin, line);
           int divisor = stringToInteger(line);
           
           int ret = Solution().divide(dividend, divisor);
   
           string out = to_string(ret);
           cout << out << endl;
       }
       return 0;
   }
   ```

2. Power of Two - Esay

   [site](https://leetcode.com/problems/power-of-two/)

   Given an integer, write a function to determine if it is a power of two.

   **Example 1:**

   ```
   Input: 1
   Output: true 
   Explanation: 20 = 1
   ```

   **Example 2:**

   ```
   Input: 16
   Output: true
   Explanation: 24 = 16
   ```

   **Example 3:**

   ```
   Input: 218
   Output: false
   ```

   ```c++
   class Solution {
   public:
       
       bool isPowerOfTwo(int n) {
           if(n<=0) return false;
           return !(n&(n-1));
   //         if(n == 1)
   //             return true;
   //         if(n == 0)
   //             return false;
           
   //         while(n % 2 == 0)
   //             n = n/2;
   //         cout << n << endl;
   //         if(n == 1)
   //             return true;
   //         return false;
       }
   };
   ```

   

3. s

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

   