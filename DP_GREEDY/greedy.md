# Greedy

큰 수 만들기

[Original MD](/Users/yeokyuli/Google Drive/KyuLi/구글/Data-Structure/Algorithm Study/20191222.md)



```c++
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>

using namespace std;

//number.length() - (i+1) >=k

string solution(string number, int k) {
    string answer = "";
    int resultLen = number.length() - k;
    int pos = 0;
    while(k !=0) // resultLen > 0
    {
        int maxValue = -1;
        int maxPos = 0;
         for(int i = pos; i <= (pos+k) ; i++)
        {
                if (maxValue < number[i] ) 
                {
                    if(number.length() - i == k && pos==0) 
                        return number.substr(k, number.length());
                    maxValue = number[i];
                    maxPos = i;
                }
        }
        k = k - ( maxPos- pos);
        pos = maxPos+1;

        cout << maxValue-'0' << " " << k << endl;
        if(resultLen == answer.length() )
            return answer;
        if(k==0)
            answer += number.substr(pos-1, number.length());
        else
            answer += maxValue;  
    }
    return answer;
}
```









```c++

```



```c++

```



```c++

```

