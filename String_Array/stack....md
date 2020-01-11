# Stack



```c++
/*
2019.09.28
 Stack - array

*/
#include <iostream>

using namespace std;

class MinStack {
private:
    int arr[100];
    vector<int> st;
    stack<int> stack;
    int minNum = 100000;
    int location = 0;
public:
    /** initialize your data structure here. */
    MinStack() {
        
    }
    
    void push(int x) {
        arr[location] = x;
        location++;
        if(minNum > x){
            minNum = x;
        }
    }
    
    void pop() { // remove
        if(location <= 0)
            return;
        
        if(arr[location-1] == minNum){
            minNum = arr[0];
            for(int i = 1 ; i < location-1; i++)
            {
                if(minNum > arr[i])
                    minNum = arr[i];
            }
        }
        arr[location--];
    }
    
    int top() { //return
        if(location <= 0)
            return -1;
        return arr[location-1];
        
    }
    
    int getMin() {
        return minNum;
    }
};

int main()
{
    MinStack st;
    st.push(3);
    st.push(2);
    st.pop();
    cout << st.top() << endl;
    cout << st.getMin() << endl;

    return 0;
}
```



1. Min stack - Esay

   Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

   - push(x) -- Push element x onto stack.
   - pop() -- Removes the element on top of the stack.
   - top() -- Get the top element.
   - getMin() -- Retrieve the minimum element in the stack.

    

   **Example:**

   ```
   MinStack minStack = new MinStack();
   minStack.push(-2);
   minStack.push(0);
   minStack.push(-3);
   minStack.getMin();   --> Returns -3.
   minStack.pop();
   minStack.top();      --> Returns 0.
   minStack.getMin();   --> Returns -2.
   ```

    

   ```c++
   class MinStack {
   private:
       int arr[10000];
       int location = 0;
       int minNum = INT_MAX ;
       
   public:
       /** initialize your data structure here. */
       MinStack() {
           
       }
       
       void push(int x) {
           arr[location] = x;
           location++;
           if(location == 1)
               minNum = x;
           else{
               if(minNum > x)
                   minNum = x;
           }
       }
       
       void pop() {
           if(location <= 0)
              return;
           
           if(arr[location-1] == minNum){
               minNum = arr[0];
               for(int i = 0; i < location-1; i++)
                   if(minNum > arr[i])
                       minNum = arr[i];
           }
           arr[location--];
       }
       
       int top() {
           if(location <= 0)
           {
               return -1;
           }
           return arr[location-1];
       }
       
       int getMin() {
           return minNum;
       }
   };
   
   /**
    * Your MinStack object will be instantiated and called as such:
    * MinStack* obj = new MinStack();
    * obj->push(x);
    * obj->pop();
    * int param_3 = obj->top();
    * int param_4 = obj->getMin();
    */
   ```

   

2. 10828 - 스택

   [site](https://www.acmicpc.net/problem/10828)

   | 시간 제한               | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
   | :---------------------- | :---------- | :---- | :---- | :-------- | :-------- |
   | 0.5 초 (추가 시간 없음) | 256 MB      | 58268 | 22289 | 16298     | 40.244%   |

   ## 문제

   정수를 저장하는 스택을 구현한 다음, 입력으로 주어지는 명령을 처리하는 프로그램을 작성하시오.

   명령은 총 다섯 가지이다.

   - push X: 정수 X를 스택에 넣는 연산이다.
   - pop: 스택에서 가장 위에 있는 정수를 빼고, 그 수를 출력한다. 만약 스택에 들어있는 정수가 없는 경우에는 -1을 출력한다.
   - size: 스택에 들어있는 정수의 개수를 출력한다.
   - empty: 스택이 비어있으면 1, 아니면 0을 출력한다.
   - top: 스택의 가장 위에 있는 정수를 출력한다. 만약 스택에 들어있는 정수가 없는 경우에는 -1을 출력한다.

   ## 입력

   첫째 줄에 주어지는 명령의 수 N (1 ≤ N ≤ 10,000)이 주어진다. 둘째 줄부터 N개의 줄에는 명령이 하나씩 주어진다. 주어지는 정수는 1보다 크거나 같고, 100,000보다 작거나 같다. 문제에 나와있지 않은 명령이 주어지는 경우는 없다.

   ## 출력

   출력해야하는 명령이 주어질 때마다, 한 줄에 하나씩 출력한다.

   ## 예제 입력 1 복사

   ```
   14
   push 1
   push 2
   top
   size
   empty
   pop
   pop
   pop
   size
   empty
   pop
   push 3
   empty
   top
   ```

   ## 예제 출력 1 복사

   ```
   2
   2
   0
   2
   1
   -1
   0
   1
   -1
   0
   3
   ```

   ## 예제 입력 2 복사

   ```
   7
   pop
   top
   push 123
   top
   pop
   top
   pop
   ```

   ## 예제 출력 2 복사

   ```
   -1
   -1
   123
   123
   -1
   -1
   ```

   ```c++
   //
   //  스택2.cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 20/03/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   
   #include <iostream>
   #include <stack>
   #include <string>
   using namespace std;
   int main() {
       int cnt, num;
       string command;
       cin >> cnt;
       stack<int> st;
       while(cnt--){
           cin >> command;
           if (command == "push")
           {
               cin >> num;
               st.push(num);
           }
           else if(command == "top"){
               if(st.empty()){
                   cout << "-1" << endl;
               }
               else{
                   cout << st.top() << endl;
               }
           }
           else if(command == "size"){
               cout << st.size() << endl;
           }
           else if(command == "empty"){
               if (st.empty()){
                   cout << "1" << endl;
               }
               else
                   cout << "0" << endl;
           }
           else if(command == "pop"){
               if (st.empty()){
                   cout << "-1" << endl;
               }
               else{
                   cout << st.top() << endl;
                   st.pop();
               }
           }
       }
       return 0;
   }
   
   ```

3. 10845 - 큐

   [site](https://www.acmicpc.net/problem/10845)

   | 시간 제한               | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
   | :---------------------- | :---------- | :---- | :---- | :-------- | :-------- |
   | 0.5 초 (추가 시간 없음) | 256 MB      | 33336 | 15468 | 12024     | 49.526%   |

   ## 문제

   정수를 저장하는 큐를 구현한 다음, 입력으로 주어지는 명령을 처리하는 프로그램을 작성하시오.

   명령은 총 여섯 가지이다.

   - push X: 정수 X를 큐에 넣는 연산이다.
   - pop: 큐에서 가장 앞에 있는 정수를 빼고, 그 수를 출력한다. 만약 큐에 들어있는 정수가 없는 경우에는 -1을 출력한다.
   - size: 큐에 들어있는 정수의 개수를 출력한다.
   - empty: 큐가 비어있으면 1, 아니면 0을 출력한다.
   - front: 큐의 가장 앞에 있는 정수를 출력한다. 만약 큐에 들어있는 정수가 없는 경우에는 -1을 출력한다.
   - back: 큐의 가장 뒤에 있는 정수를 출력한다. 만약 큐에 들어있는 정수가 없는 경우에는 -1을 출력한다.

   ## 입력

   첫째 줄에 주어지는 명령의 수 N (1 ≤ N ≤ 10,000)이 주어진다. 둘째 줄부터 N개의 줄에는 명령이 하나씩 주어진다. 주어지는 정수는 1보다 크거나 같고, 100,000보다 작거나 같다. 문제에 나와있지 않은 명령이 주어지는 경우는 없다.

   ## 출력

   출력해야하는 명령이 주어질 때마다, 한 줄에 하나씩 출력한다.

   ## 예제 입력 1 복사

   ```
   15
   push 1
   push 2
   front
   back
   size
   empty
   pop
   pop
   pop
   size
   empty
   pop
   push 3
   empty
   front
   ```

   ## 예제 출력 1 복사

   ```
   1
   2
   2
   0
   1
   2
   -1
   0
   1
   -1
   0
   3
   ```

   ```c++
   //
   //  큐(10845).cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 27/03/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   
   #include <iostream>
   #include <queue>
   #include <string>
   using namespace std;
   int main()
   {
       int cnt, num;
       queue<int> que;
       string command;
       cin >> cnt;
       while(cnt--){
           cin >> command;
           if(command == "push"){
               cin >> num;
               que.push(num);
           }
           else if(command == "pop"){
               if(que.empty())
                   cout << "-1" << endl;
               else{
                   cout << que.front() << endl;
                   que.pop();
               }
           }
           else if(command == "size"){
               cout << que.size() << endl;
           }
           else if(command == "empty"){
               if(que.empty()){
                   cout << "1" << endl;
               }
               else
                   cout << "0" << endl;
           }
           else if(command == "front"){
               if(que.empty()){
                   cout << "-1" << endl;
               }
               else
                   cout << que.front() << endl;
           }
           else if(command == "back"){
               if(que.empty()){
                   cout << "-1" << endl;
               }
               else
                   cout << que.back() << endl;
           }
       }
       
   }
   
   ```

   1. ```c++
      #include <iostream>
      using namespace std;
      class Queue{
          
      private:
          int que[1000];
          int frist = -1;
          int rear = -1;
       
      public:
          int front(){
              return que[frist];
          }
          int back()
          {
              return que[rear];
          }
          void pop_front()
          {
              frist++;
          }
          void push_back(int x){
              if(frist == -1){
                  frist = 0;
              }
              rear++;
              que[rear] = x;
          }
          bool empty(){
              if(frist == -1 || (rear-frist)==0)
                  return false;
              return true;
          }
          int size(){
              if(frist == -1 || (rear-frist)==0)
                  return -1;
              return (rear-frist)+1;
          }
          
      };
      int main()
      {
          Queue que;
          
          cout << "que size ?"<< que.size() << endl;
          cout << "que empty ? " << que.empty() << endl;
          que.push_back(1);
          que.push_back(10);
          cout << "que front " << que.front() << endl;
          cout << "que back " << que.back() << endl;
          que.push_back(5);
          que.pop_front();
          cout << "que front " << que.front() << endl;
          que.push_back(6);
          cout << "que back " << que.back() << endl;
          cout << "que size " << que.size() << endl;
           
      
          return 0;
      }
      ```

4. 10866 - 덱

   [site](https://www.acmicpc.net/problem/10866)

   | 시간 제한               | 메모리 제한 | 제출  | 정답 | 맞은 사람 | 정답 비율 |
   | :---------------------- | :---------- | :---- | :--- | :-------- | :-------- |
   | 0.5 초 (추가 시간 없음) | 256 MB      | 13585 | 6770 | 5711      | 54.750%   |

   ## 문제

   정수를 저장하는 덱(Deque)를 구현한 다음, 입력으로 주어지는 명령을 처리하는 프로그램을 작성하시오.

   명령은 총 여덟 가지이다.

   - push_front X: 정수 X를 덱의 앞에 넣는다.
   - push_back X: 정수 X를 덱의 뒤에 넣는다.
   - pop_front: 덱의 가장 앞에 있는 수를 빼고, 그 수를 출력한다. 만약, 덱에 들어있는 정수가 없는 경우에는 -1을 출력한다.
   - pop_back: 덱의 가장 뒤에 있는 수를 빼고, 그 수를 출력한다. 만약, 덱에 들어있는 정수가 없는 경우에는 -1을 출력한다.
   - size: 덱에 들어있는 정수의 개수를 출력한다.
   - empty: 덱이 비어있으면 1을, 아니면 0을 출력한다.
   - front: 덱의 가장 앞에 있는 정수를 출력한다. 만약 덱에 들어있는 정수가 없는 경우에는 -1을 출력한다.
   - back: 덱의 가장 뒤에 있는 정수를 출력한다. 만약 덱에 들어있는 정수가 없는 경우에는 -1을 출력한다.

   ## 입력

   첫째 줄에 주어지는 명령의 수 N (1 ≤ N ≤ 10,000)이 주어진다. 둘쨰 줄부터 N개의 줄에는 명령이 하나씩 주어진다. 주어지는 정수는 1보다 크거나 같고, 100,000보다 작거나 같다. 문제에 나와있지 않은 명령이 주어지는 경우는 없다.

   ## 출력

   출력해야하는 명령이 주어질 때마다, 한 줄에 하나씩 출력한다.

   ## 예제 입력 1 복사

   ```
   15
   push_back 1
   push_front 2
   front
   back
   size
   empty
   pop_front
   pop_back
   pop_front
   size
   empty
   pop_back
   push_front 3
   empty
   front
   ```

   ## 예제 출력 1 복사

   ```
   2
   1
   2
   0
   2
   1
   -1
   0
   1
   -1
   0
   3
   ```

   ```c++
   //
   //  덱(10866).cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 29/03/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   #include <iostream>
   #include <deque>
   #include <string>
   using namespace std;
   
   int main()
   {
       
       int cnt;
       string command;
       int num;
       cin >> cnt;
       deque<int> deq;
       while(cnt--){
           cin >> command;
           if(command == "push_front"){
               cin >> num;
               deq.push_front(num);
           }
           else if(command == "push_back"){
               cin>>num;
               deq.push_back(num);
           }
           else if(command == "pop_front"){
               if(!deq.empty()){
                   cout << deq.front() << endl;
                   deq.pop_front();
               }
               else
                   cout << -1 << endl;
           }
           else if(command == "pop_back"){
               if(!deq.empty()){
                   cout << deq.back() << endl;
                   deq.pop_back();
               }
               else
                   cout << -1 << endl;
           }
           else if(command == "size")
               cout << deq.size() << endl;
           else if(command == "empty"){
               if(deq.empty()) cout << 1 << endl;
               else cout << 0 << endl;
           }
           else if(command == "front"){
               if(deq.empty()) cout << -1 << endl;
               else cout << deq.front() << endl;
           }
           else if(command == "back"){
               if(deq.empty()) cout << -1 << endl;
               else cout << deq.back() << endl;
           }
       }
       return 0;
   }
   
   
   ```

   