# Math

1. Power of Three - easy

   [site](https://leetcode.com/problems/power-of-three/)

   Given an integer, write a function to determine if it is a power of three.

   **Example 1:**

   ```
   Input: 27
   Output: true
   ```

   **Example 2:**

   ```
   Input: 0
   Output: false
   ```

   **Example 3:**

   ```
   Input: 9
   Output: true
   ```

   **Example 4:**

   ```
   Input: 45
   Output: false
   ```

   **Follow up:**
   Could you do it without using any loop / recursion?

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

   

2. **Happy Number** - Easy

   Write an algorithm to determine if a number is "happy".

   A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

   **Example:** 

   ```
   Input: 19
   Output: true
   Explanation: 
   12 + 92 = 82
   82 + 22 = 68
   62 + 82 = 100
   12 + 02 + 02 = 1
   ```

   ```c++
   #include <string>
   //to_string, stoi, char -'0'
   class Solution {
   private:
       int nextNum(int n)
       {
           cout << n << " ";
           int next = 0; 
           while(n!=0)
           {
               next += pow(n % 10,2);
               n /= 10;
           }
           return next;       
       }
   public:
       bool isHappy(int n) {
           int cur = nextNum(n);
           int fast = nextNum(nextNum(n));
           
           
           while(cur != fast)
           {
               cur = nextNum(cur);
               fast = nextNum(nextNum(fast));
           }
           
           
           return fast == 1;
       }
   
   };
   
   
   
   /*
   
           while(n!=0)
           {
               cout << n % 10;
               n /= 10;
           }
           */
   ```

   

3. 2진수 8진수 성공 - 1373

   [site](https://www.acmicpc.net/problem/1373)

   | 시간 제한 | 메모리 제한 | 제출  | 정답 | 맞은 사람 | 정답 비율 |
   | :-------- | :---------- | :---- | :--- | :-------- | :-------- |
   | 1 초      | 128 MB      | 11398 | 3946 | 3199      | 38.074%   |

   ## 문제

   2진수가 주어졌을 때, 8진수로 변환하는 프로그램을 작성하시오.

   ## 입력

   첫째 줄에 2진수가 주어진다. 주어지는 수의 길이는 1,000,000을 넘지 않는다.

   ## 출력

   첫째 줄에 주어진 수를 8진수로 변환하여 출력한다.

   ## 예제 입력 1 복사

   ```
   11001100
   ```

   ## 예제 출력 1 복사

   ```
   314
   ```

   ```c++
   //
   //  2진수 8진수(1373).cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 01/04/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   #include <iostream>
   #include <string>
   using namespace std;
   int main()
   {
       
       string str;
       cin >> str;
       
       if(str.length()%3 == 1)
           str = "00" + str;
       else if(str.length()%3 == 2)
           str =  "0" + str;
       
   
       for(int i = str.length()%3 ; i < str.length(); i= i+3){
           cout << (str[i] - '0') *4 + (str[i+1] - '0')*2 + str[i+2]-'0';
       }
       return 0;
   }
   
   ```

   

4. 1934 최소공배수

   [site](https://www.acmicpc.net/problem/1934)

   | 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
   | :-------- | :---------- | :---- | :---- | :-------- | :-------- |
   | 1 초      | 128 MB      | 17795 | 10062 | 8559      | 58.760%   |

   ## 문제

   두 자연수 A와 B에 대해서, A의 배수이면서 B의 배수인 자연수를 A와 B의 공배수라고 한다. 이런 공배수 중에서 가장 작은 수를 최소공배수라고 한다. 예를 들어, 6과 15의 공배수는 30, 60, 90등이 있으며, 최소 공배수는 30이다.

   두 자연수 A와 B가 주어졌을 때, A와 B의 최소공배수를 구하는 프로그램을 작성하시오.

   ## 입력

   첫째 줄에 테스트 케이스의 개수 T(1 ≤ T ≤ 1,000)가 주어진다. 둘째 줄부터 T개의 줄에 걸쳐서 A와 B가 주어진다. (1 ≤ A, B ≤ 45,000)

   ## 출력

   첫째 줄부터 T개의 줄에 A와 B의 최소공배수를 입력받은 순서대로 한 줄에 하나씩 출력한다.

   ## 예제 입력 1 복사

   ```
   3
   1 45000
   6 10
   13 17
   ```

   ## 예제 출력 1 복사

   ```
   45000
   30
   221
   ```

   ```c++
   //
   //  최소공배수(1934).cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 31/03/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   #include <iostream>
   
   using namespace std;
   
   int gcd(int a , int b){
       return b==0 ? a : gcd(b, a%b);
   }
   int main()
   {
       int cnt, a, b;
       cin >> cnt;
       while(cnt--){
           cin >> a  >> b;
           cout << (a*b)/gcd(a,b) << endl;
       }
       return 0;
   }
   
   ```

5. 2609 최대공약수와 최소공배수

   [site](https://www.acmicpc.net/problem/2609)

   | 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
   | :-------- | :---------- | :---- | :---- | :-------- | :-------- |
   | 1 초      | 128 MB      | 21398 | 13594 | 11125     | 65.261%   |

   ## 문제

   두 개의 자연수를 입력받아 최대 공약수와 최소 공배수를 출력하는 프로그램을 작성하시오.

   ## 입력

   첫째 줄에는 두 개의 자연수가 주어진다. 이 둘은 10,000이하의 자연수이며 사이에 한 칸의 공백이 주어진다.

   ## 출력

   첫째 줄에는 입력으로 주어진 두 수의 최대공약수를,둘째 줄에는 입력으로 주어진 두 수의 최소 공배수를 출력한다.

   ## 예제 입력 1 복사

   ```
   24 18
   ```

   ## 예제 출력 1 복사

   ```
   6
   72
   ```

   ```c++
   //
   //  최대공약수과 최소공배수(2609).cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 31/03/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   #include <iostream>
   #include <algorithm>
   using namespace std;
   
   int gcd (int a , int b){
       return b == 0 ? a : gcd (b, a%b);
   }
   int main()
   {
       
       int a , b;
       cin >> a >> b;
       int c;
       c = gcd(a,b);
       cout << c << endl;
       cout << (a*b)/c << endl;
       return 0;
   }
   
   ```

6. 9613 - GCD 합

   [site](https://www.acmicpc.net/problem/9613)  

   | 시간 제한 | 메모리 제한 | 제출  | 정답 | 맞은 사람 | 정답 비율 |
   | :-------- | :---------- | :---- | :--- | :-------- | :-------- |
   | 1 초      | 128 MB      | 11055 | 3736 | 3046      | 36.646%   |

   ## 문제

   양의 정수 n개가 주어졌을 때, 가능한 모든 쌍의 GCD의 합을 구하는 프로그램을 작성하시오.

   ## 입력

   첫째 줄에 테스트 케이스의 개수 t (1 ≤ t ≤ 100)이 주어진다. 각 테스트 케이스는 한 줄로 이루어져 있다. 각 테스트 케이스는 수의 개수 n (1 < n ≤ 100)가 주어지고, 다음에는 n개의 수가 주어진다. 입력으로 주어지는 수는 1000000을 넘지 않는다.

   ## 출력

   각 테스트 케이스마다 가능한 모든 쌍의 GCD의 합을 출력한다.

   ## 예제 입력 1 복사

   ```
   3
   4 10 20 30 40
   3 7 5 12
   3 125 15 25
   ```

   ## 예제 출력 1 복사

   ```
   70
   3
   35
   ```

   ```c++
   //
   //  GCD 합(9613).cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 31/03/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   #include <iostream>
   using namespace std;
   int num[100]{0};
   int gcd(int a , int b){
       return b == 0 ? a : gcd(b, a%b);
   }
   int main()
   {
       
       int cnt;
       cin >> cnt;
       while(cnt--){
           int arrNum;
           cin >> arrNum;
           for(int i = 0 ; i < arrNum; i++)
               cin >> num[i];
           
           long long result = 0;
           for(int i = 0 ; i< arrNum-1; i++){
               for(int j = i+1 ; j < arrNum ; j++){
                   result += gcd(num[i], num[j]);
               }
           }
           cout << result << endl;
       }
       return 0;
   }
   
   ```

7. 10430 - 나머지

   [site](https://www.acmicpc.net/problem/10430)

   | 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
   | :-------- | :---------- | :---- | :---- | :-------- | :-------- |
   | 1 초      | 256 MB      | 67002 | 39863 | 36595     | 60.889%   |

   ## 문제

   (A+B)%C는 (A%C + B%C)%C 와 같을까?

   (A×B)%C는 (A%C × B%C)%C 와 같을까?

   세 수 A, B, C가 주어졌을 때, 위의 네 가지 값을 구하는 프로그램을 작성하시오.

   ## 입력

   첫째 줄에 A, B, C가 순서대로 주어진다. (2 ≤ A, B, C ≤ 10000)

   ## 출력

   첫째 줄에 (A+B)%C, 둘째 줄에 (A%C + B%C)%C, 셋째 줄에 (A×B)%C, 넷째 줄에 (A%C × B%C)%C를 출력한다.

   ## 예제 입력 1 복사

   ```
   5 8 4
   ```

   ## 예제 출력 1 복사

   ```
   1
   1
   0
   0
   ```

   ```c++
    //
   //  나머지(10430).cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 31/03/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   #include <iostream>
   using namespace std;
   
   int main()
   {
       int a, b , c;
       
       cin >> a >> b >> c;
       
       cout << (a+b)%c << endl;
       cout << ((a%c) + (b%c))%c << endl;
       cout << (a*b)%c << endl;
       cout << ((a%c) * (b%c))%c << endl;
       return 0;
   }
   
   ```

8. dd

   ```c++
   
   ```

9. dd

   ```c++
   
   ```

10. dd

    ```c++
    
    ```

11. dd

    ```c++
    
    ```

12. dd

    ```c++
    
    ```

13. dd

    ```c++
    
    ```

14. dd

    ```c++
    
    ```

15. dd

    ```c++
    
    ```

16. dd

    ```c++
    
    ```

17. dd

    ```c++
    
    ```

18. dd

    ```c++
    
    ```

19. dd

    ```c++
    
    ```

20. dd

    ```c++
    
    ```

    