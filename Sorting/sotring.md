# Sorting

1. bubble sort - 1377 

   [site](https://www.acmicpc.net/problem/1377)

   | 시간 제한 | 메모리 제한 | 제출 | 정답 | 맞은 사람 | 정답 비율 |
   | :-------- | :---------- | :--- | :--- | :-------- | :-------- |
   | 2 초      | 128 MB      | 5723 | 1469 | 1153      | 30.788%   |

   ## 문제

   영식이는 다음과 같은 버블 소트 프로그램을 C++로 작성했다.

   ```
   `bool` `change = ``false``;``for` `(``int` `i=1; i<=n+1; i++) {``  ``change = ``false``;``  ``for` `(``int` `j=1; j<=n-i; j++) {``    ``if` `(a[j] > a[j+1]) {``      ``change = ``true``;``      ``swap(a[j], a[j+1]);``    ``}``  ``}``  ``if` `(change == ``false``) {``    ``cout << i << ``'\n'``;``    ``break``;``  ``}``}`
   ```

   위 소스에서 n은 배열의 크기이고, a는 수가 들어있는 배열이다. 수는 배열의 1번방부터 채운다.

   위와 같은 소스를 실행시켰을 때, 어떤 값이 출력되는지 구하는 프로그램을 작성하시오.

   ## 입력

   첫째 줄에 N이 주어진다. N은 500,000보다 작거나 같은 자연수이다. 둘째 줄부터 N개의 줄에 A[1]부터 A[N]까지 하나씩 주어진다. A에 들어있는 수는 1,000,000보다 작거나 같은 자연수 또는 0이다.

   ## 출력

   정답을 출력한다.

   ## 예제 입력 1 복사

   ```
   5
   10
   1
   5
   2
   3
   ```

   ## 예제 출력 1 복사

   ```
   3
   ```

   ```c++
   //
   //  버블 소트 (1377).cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 09/04/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   
   #include <iostream>
   #include <algorithm>
   #include <vector>
   using namespace std;
   int main()
   {
       cin.sync_with_stdio(false);
       int cnt;
       cin >> cnt;
       vector<pair<int,int>> v(cnt);
       
       for(int i = 0 ; i < cnt ; i++){
           cin >> v[i].first;
           v[i].second = i;
       }
       sort(v.begin(), v.end());
       int result = 0;
       for(int i = 0 ; i < cnt ; i++)
           result = max(result, v[i].second - i);
       
       cout << result + 1 << endl;
       
       return 0;
   }
   
   ```

2. s

   ```c++
   
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

   