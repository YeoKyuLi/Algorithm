# Uncategorized

1. **Fizz Buzz** - Easy

   [site](https://leetcode.com/problems/fizz-buzz/)

   Write a program that outputs the string representation of numbers from 1 to *n*.

   But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.

   **Example:**

   ```
   n = 15,
   
   Return:
   [
       "1",
       "2",
       "Fizz",
       "4",
       "Buzz",
       "Fizz",
       "7",
       "8",
       "Fizz",
       "Buzz",
       "11",
       "Fizz",
       "13",
       "14",
       "FizzBuzz"
   ]
   ```

   ```c++
   #include<string>
   
   class Solution {
   public:
       vector<string> fizzBuzz(int n) {
           vector<string> result;
           string three = "Fizz";
           string five = "Buzz";
   
           for(int i = 1 ; i <= n ; i++){
               if(i % 3 == 0 && i%5 == 0){
                   cout << "1";
                   result.push_back(three + five);
               }
               else if(i % 3 == 0 ){
                   cout << "2";
                   result.push_back(three);
               }
               else if(i % 5 == 0 ){
                   cout << "3";
                  result.push_back(five);
               }
               else{
                   cout << "4";
                   result.push_back(to_string(i));
               }
               cout << endl;
                  
           }
   
           return result;
       }
   };
   ```

   

2. s