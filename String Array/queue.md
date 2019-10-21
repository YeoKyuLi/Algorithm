# Queue





```c++
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

